# Rocky Linux VM using Vagrant and VMware

## Overview
This project demonstrates how to create a Rocky Linux virtual machine using Vagrant and VMware Workstation.

## Features
- Automated VM creation using Vagrant
- Rocky Linux 8
- 2 vCPU
- 4 GB RAM
- VMware Workstation provider
- SSH access to the VM
- Root login configuration for lab practice

## Prerequisites
- Vagrant
- VMware Workstation
- Vagrant VMware plugin

## Start the VM

```bash
vagrant up --provider=vmware_workstation
