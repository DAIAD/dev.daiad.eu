# README

This repository contains scripts (mainly ansible automation) for the deployment of `dev.daiad.eu`.

## Prerequisites for hosts

Before using a host as a target for an ansible playbook, some minimal prerequisites must be fullfilled. 
For the scope of this document, we assume that all hosts run on an Ubuntu 14.04 (trusty) platform. 

Ensure the following:

 1. The `network-manager` daemon is disabled. You should override the `upstart` configuration (see http://askubuntu.com/questions/19320/how-to-enable-or-disable-services). 
 2. All IPv4 network interfaces must be configured via `/etc/network/interfaces` stanzas. The primary IPv4 interface (e.g `eth1`) should be assigned a valid address into `10.0.2.0/24`.
 3. The default user `user` should be a password-less sudoer (tweak `/etc/sudoers` if needed). 

If hosts do not have access to the public IPv4 internet (e.g if they only connect to the local `10.0.2.0/24` network), then you should provide a NAT'ed gateway through Ansible's control-node. So, additionaly, ensure that:
 1. The control-node can act as an IPv4 forwarder (`net.ipv4.ip_forward=1`)
 2. The control-node will masquerade (SNAT) incoming traffic from the internal network
 3. All hosts (i.e. the controlled nodes) are using the control-node as default gateway

## Deployment 

Configure hosts and groups in `hosts.conf`.

Prepare target hostnames and target user:

    ansible-playbook -v -i hosts.conf prepare.yml

Setup groups according to their role:

    ansible-playbook -v -i hosts.conf setup-roles.yml

