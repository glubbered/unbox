# A Virtual Machine for Ruby on Rails Core Development

## Introduction

This project automates the setup of a development environment for Ruby on Rails core development. This is the easiest way to build a box with everything ready to start hacking on your pull request, all in an isolated virtual machine.

## Requirements

* [VirtualBox](https://www.virtualbox.org)

* [Vagrant](http://vagrantup.com)

## How To Build The Virtual Machine

Building the virtual machine is this easy:

    host $ git clone https://github.com/rails/rails-dev-box.git
    host $ cd rails-dev-box
    host $ vagrant up

That's it.

If the base box is not present that command fetches it first. The setup itself takes about 3 minutes in my MacBook Air. After the installation has finished, you can access the virtual machine with

    host $ vagrant ssh
    Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic-pae i686)
    ...
    vagrant@rails-dev-box:~$

Port 3000 in the host computer is forwarded to port 3000 in the virtual machine. Thus, applications running in the virtual machine can be accessed via localhost:3000 in the host computer.

## What's In The Box

* Git

* RVM

* Ruby 1.9.3 (binary RVM install)

* Bundler

* SQLite3, MySQL, and Postgres

* System dependencies for nokogiri, sqlite3, mysql, mysql2, and pg

* Databases and users needed to run the Active Record test suite

* Node.js for the asset pipeline

* Memcached

## Recommended Workflow

The recommended workflow is

* edit in the host computer and

* test within the virtual machine.

Just clone your Rails fork in the very directory of the Rails development box in the host computer:

    host $ ls
    README.md   Vagrantfile puppet
    host $ git clone git@github.com:<your username>/rails.git

Vagrant mounts that very directory as _/vagrant_ within the virtual machine:

    vagrant@rails-dev-box:~$ ls /vagrant
    puppet  rails  README.md  Vagrantfile

so we are ready to go to edit in the host, and test in the virtual machine.

This workflow is convenient because in the host computer you normally have your editor of choice fine-tuned, Git configured, and SSH keys in place.

## Virtual Machine Management

When done just log out with `^D` and suspend the virtual machine

    host $ vagrant suspend

then, resume to hack again

    host $ vagrant resume

Run

    host $ vagrant halt

to shutdown the virtual machine, and

    host $ vagrant up

to boot it again.

You can find out the state of a virtual machine anytime by invoking

    host $ vagrant status

Finally, to completely wipe the virtual machine from the disk **destroying all its contents**:

    host $ vagrant destroy # DANGER: all is gone

Please check the [Vagrant documentation](http://vagrantup.com/v1/docs/index.html) for more information on Vagrant.

## Customizations By Chris

Added a default shared path pointing to `~/Sites` on the host and `/home/vagrant/Sites` on the guest. `~/Sites` used 
to be standard in OS X pre-Mountain Lion; now it's back. If the directory doesn't exist, Vagrant will create it.

This means you should clone your rails apps into `~/Sites` to work on them.

Set the default HTTP forwarded port to `:3030` instead of `:3000`. This keeps `:3000` open for local web apps not run 
in the VM.

## Running a Rails App

First, `vagrant ssh` then `cd ./Sites`. `git clone [rails app]` then `bundle`. Next `script/rails server`.
