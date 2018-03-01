# Gratitude and Notice of Theft

I am basically taking Khelil's stuff and using GitHub to organize it into my lab environment and learning a ton of new stuff.

https://github.com/ksator/junos-automation-with-ansible <--- His stuff is located here.

https://github.com/ksator/lab_management <--- And even more stuff here.

I don't know that I'll ever get to the awesome part of this but I keep working on it.

# Install instructions

Build a basic Ubuntu 16.04 Server and don't update it. Follow the instructions below.

## Get the content of the remote repository locally

sudo -s
git clone https://github.com/packetjanitor/JNPR-FormalFabric.git
ls JNPR-FormalFabric

## Move to the local copy of the remote repo

cd JNPR-FormalFabric
sudo -s

## Install PyEZ, Jxmlease, Ansible, JSNAPy and all their dependencies

This repository has been tested using Ansible 2.4.2.0

## Run these commands on Ubuntu 16.04 to install these tools:

sudo -s
apt-get update
apt-get upgrade
apt-get install -y python-dev libxml2-dev python-pip libxslt1-dev build-essential libssl-dev libffi-dev git
pip install junos-eznc jxmlease wget jsnapy ansible==2.4.2.0 requests ipaddress cryptography 
ansible-galaxy install Juniper.junos,1.4.3

Check the Ansible version:

ansible --version

Verify you have the Juniper.junos role:

ls /etc/ansible/roles/

This repository has been tested using the version 1.4.3 of the Juniper.junos role available on Galaxy.
Use this command to see the name and version of each role installed:

ansible-galaxy list

## Permission problems

I know running everything with sudo -s will put alot of it in root's control and thus a hassle to execute as a normal user. Here's how to solve that...

ls -al

chown <username>:<username> NameOfDirectory or FileName

## Configure NETCONF on the Junos devices

set system services netconf ssh
commit

# Repository structure
## Inventory file:

The default hosts file lives in /etc/ansible/hosts.

The inventory file we are using in this repository is hosts.

    It is at the root of the repository, so it is not at the default place.
    It defines the inventory (hosts and groups).
    It also defines the ip address of each device with the variable junos_host. This variable is re-used in the playbooks.

## Config file for ansible

There is an ansible.cfg file at the root of the repository.
It refers to our inventory file: So even if the inventory file is not in /etc/ansible/hosts, there is no need to add -i hosts to your ansible-playbook commands.

## Variables

group_vars and host_vars directories at the root of this repository define variables for hosts and for groups.
The inventory file hosts at the root of the repository also defines some variables.
The playbooks in this directory use all of them.
Some playbooks also use other variables.
In order to see all variables for a hostname, you can run this command:

ansible -m debug -a "var=hostvars['hostname']" localhost

# Travis CI Status
[![Build Status](https://travis-ci.org/packetjanitor/JNPR-FormalFabric.svg?branch=master)](https://travis-ci.org/packetjanitor/JNPR-FormalFabric)

More to come... Stay Tuned
