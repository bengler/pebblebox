# Pebblebox

Development environment for Pebblestack using a virtual machine with Vagrant.

## Install

Download and install VirtualBox (tested with 4.2.12):
https://www.virtualbox.org/wiki/Downloads

Download and install Vagrant (tested with 1.2.1):
http://downloads.vagrantup.com/

Install the Vagrant plugin for Berkshelf:
    $ vagrant plugin install berkshelf-vagrant

Build, install and start the virtual machine:
    $ vagrant up
This will take a while the first time it is run.

## Shell access
Log in to the `vagrant` user account on the virtual machine:
    $ vagrant ssh
This account can also run sudo without providing a password.

## PostgreSQL connect
Connect to PostgreSQL running inside the VM:
    $ psql -h 192.168.33.10 -U postgres -W -p 5432 [database]
The default password for the `postgres` setup by the pebble cookbook is `G8riPos1`.
