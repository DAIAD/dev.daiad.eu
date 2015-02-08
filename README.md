# README

This repository contains scripts (mainly ansible automation) for the deployment of `dev.daiad.eu`.


## Quickstart

Configure hosts and groups in `hosts.conf`.

Prepare target hostnames and target user:

    ansible-playbook -v -i hosts.conf prepare.yml

Setup groups according to their role:

    ansible-playbook -v -i hosts.conf setup-roles.yml

