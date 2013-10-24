# Pebblebox

Development environment for Pebblestack using a virtual machine with Vagrant.

## Prerequisites

### VirtualBox

Download and install VirtualBox (tested with 4.2.16): https://www.virtualbox.org/wiki/Downloads

### Vagrant

Download and install Vagrant (tested with 1.2.2): http://downloads.vagrantup.com/

### Berkshelf

Install the Vagrant plugin for Berkshelf:
```bash
$ cd ~
$ vagrant plugin install vagrant-berkshelf
```

Note: This must **not** be run from within the pebblebox directory, if you run it
there, you will only get an error message:
*Message: cannot load such file -- berkshelf/vagrant*

## Installation

### Pebblebox

Clone the Pebblebox code repository:

```bash
$ git clone git@github.com/bengler/pebblebox.git
```

Enter the directory containing the cloned repository:

```bash
$ cd pebblebox
```

### Pebblestack

First, create a subdirectory under the pebblebox directory, where
we will put code that is needed inside the virtual machine. The
pebblebox directory itself will be mirrored inside the vagrant box
at location `/vagrant`, so by creating a `src` subdirectory on the
host this will be available inside the guest at `/vagrant/src`.

```bash
$ mkdir src
$ cd src
```

Clone all needed Pebblestack repositories:

```bash
$ git clone https://github.com/bengler/brow
$ git clone https://github.com/bengler/checkpoint
```
etc.

### Vagrantfile

The file `Vagrantfile` is used to configure the virtual machine setup,
including which Chef recipies should be run to set it up.

Edit the `pebbles['repositories']` entry in the `chef.json` hash to point
to the directory containing the cloned repositories as seen by the guest:

```ruby
chef.json = {
  'pebbles' => {
    'repositories' => '/vagrant/src'
  }
}
```

Edit the `chef.run_list` hash to include all Chef recipies to be run
automatically:

```ruby
chef.run_list = [
  "recipe[apt]",
  "recipe[pebbles]",
  "recipe[pebbles::checkpoint]",
  "recipe[pebbles::brow_up]"
]
```

### Database configurations

For each pebble repository that includes a file named `config/database-example.yml`,
make a copy of this file to `config/database.yml` then edit the copy to set a password
of your choice for the `development` and `test` environments. The Chef recipies will read
these files and configure the databases accordingly.

Example:

```bash
$ cd src/checkpoint
$ cp config/database-example.yml config/database.yml
$ vi config/database.yml
```

```yaml
development:
  password: test1234

test:
  password: test1234
```

### Starting the Vagrant box

Build, install and start the virtual machine:

```bash
$ vagrant up
```

This will take a while the first time it is run, since the Linux image will
be downloaded and all Chef recipies will be run, installing needed system
packages, Ruby and the Pebblestack components.

## Shell access

Log in to the `vagrant` user account on the virtual machine:

```bash
$ vagrant ssh
```

Use *Brow* to check that the pebblestack is up and running:

```bash
$ brow status
  checkpoint (up)
  nginx/haproxy (up)

```


## HTTP access
