# Pebblebox

Development environment for Pebblestack using a virtual machine with Vagrant.

## Install

- Download and install VirtualBox (tested with 4.2.12): https://www.virtualbox.org/wiki/Downloads

- Download and install Vagrant (tested with 1.2.1): http://downloads.vagrantup.com/

- Install the Vagrant plugin for Berkshelf:

    $ vagrant plugin install berkshelf-vagrant

- Clone Pebblestack code repositories:

    $ mkdir src
    $ cd src
    $ git clone https://github.com/bengler/brow
    $ git clone https://github.com/bengler/checkpoint
    etc.

- Edit `pebbles.repositories` entry in `chef.json` inside `Vagrantfile`
  to point to the directory containing the cloned repositories.

- For each code repository that has a file `config/database-example.yml`,
  copy this file to `config/database.yml` and set a password of your
  choice for the `development` and `test` environments.

- Build, install and start the virtual machine:

    $ vagrant up

This will take a while the first time it is run.

- Once the installation process have completed successfully, comment out
  the `recipe[apt]` line from the `chef.run_list` block in `Vagrantfile`
  to speed up future chef runs somewhat, since it is only required during
  initial setup.

## Shell access

Log in to the `vagrant` user account on the virtual machine:

    $ vagrant ssh

This account can also run sudo without providing a password.

## HTTP access
