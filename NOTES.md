
# Notes

## Berkshelf Cookbook Management

http://berkshelf.com/

    $ vagrant plugin install berkshelf-vagrant
    $ berkshelf init


## VirtualBox Guest Additions

NB! This is not yet compatible with Vagrant 1.2.x!

http://kvz.io/blog/2013/01/16/vagrant-tip-keep-virtualbox-guest-additions-in-sync/

    $ vagrant plugin install vagrant-vbguest
    $ vagrant halt
    $ vagrant up


## Warnings about STDIN not being a TTY

https://github.com/myplanetdigital/vagrant-ariadne/issues/14

    $ vagrant ssh
    $ sudo su -
    # vi .profile
    -> Wrap "if `tty -s`; then" and "fi" around the "mesg n" line.

## PostgreSQL

https://github.com/opscode-cookbooks/postgresql#chef-solo-note

    $ echo -n '<password>''postgres' | openssl md5 | sed -e 's/.* /md5/'
