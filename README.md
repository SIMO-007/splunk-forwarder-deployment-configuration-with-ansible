Ansible Splunk forwarder Deployment

- Overview and prerequisites : 

This repository contains Ansible playbooks and roles to automate the deployment and configuration of Splunk Forwarder, ClamAV, sysstat, and SSL certificate setup for servers.

Splunk deployment server should be already enabled/configured

Change what needs to be changed in the main.yml in the defaults folder

add inventory with desired hosts file


Features : 

    Installs and configures Splunk Universal Forwarder

    Sets up ClamAV antivirus service with OS-specific handling

    Deploys sysstat monitoring tool setup

    Automates Let's Encrypt SSL certificate deployment for Splunk

    Supports multiple Splunk installation paths

- Prerequisites

    - Ansible 2.9 or newer installed on the control machine


    - SSH access to target servers with key authentication


    - Python installed on target hosts (for Ansible modules)
    

    - Proper inventory file with hosts and variables configured

- Inventory Example : 


[servers_22]

x.x.x.x ansible_user={user} ansible_ssh_private_key_file=/path/to/your/key.pem ansible_port=x   (change IP & ssh port)




- Usage
Run a specific playbook

   ansible-playbook -i inventories/your_inventory_file sysstat.yml
   
   
- Directory Structure

Tasks

|

├── ubuntu_deploy.yml     # splunk forwarder deployment for ubuntu servers

├── alma_deploy.yml       # splunk forwarder deployment for Alma Linux servers

├── scripts-execute.yml   # Playbook to execute custom scripts (login + clamav log scripts)

├── cert-execute.yml      # Playbook for SSL certificate logs 

├── clamav-setup.yml      # Playbook for ClamAV installation 

└── sysstat.yml           # Playbook for sysstat installation (essential library for system info logs)


- Playbook execution order for new servers 

ubuntu_deploy.yml/alma_deploy.yml  ==>  sysstat.yml ==>  clamav-setup.yml ==> scripts-execute.yml ==> cert-execute.yml
