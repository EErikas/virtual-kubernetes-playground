# Kubernetes Virtual playground
A set of Vagrant and Ansible scripts that create a virtual Kubernetes cluster on the VirtualBox VMs


## Pre-requisites
Before setting up the environment you need to have the following packages setup:
- [VirtualBox](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/index.html)

## Base image set up
To set up the base image, navigate to `base/` directory and do the following commands:
```bash
vagrant up --provision
vagrant package --output base.box
vagrant box add base base.box --force
vagrant destroy -f
```

## Starting the infrastructure
To start the infrastructure use the following command from the root of the project:
```bash
vagrant up
```
After the infrastructure is built you can use the following command to access the `master` node
```
vagrant ssh master
```