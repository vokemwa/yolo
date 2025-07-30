# **Step by Step Ansible Implementation with vagrant**

### Install vagrant and Ansible on your host machine

### Clone the React JS app for IP2 or just reuse the app by creating a different branch in your git repository

### Create the Vagrantfile in your root directory of your application

### Create the hosts file in the root  directory

### Create the roles folder in the root directory

### Create ansible.cfg file in the root directory

### Vagrantfile specifies and downloads the base box image from vagrant cloud and spins up a vm based on the base image using ansible installed in the host machine
-It also calls the playbook.yaml that has configurations to various tasks of the application

### ansible.cfg file 
-Tells ansible to use the file named hosts as the inventory file
-Sets the default SSH user for Ansible to connect to managed machines.
-Specifies the private SSH key used to connect to the Vagrant-managed VM

### playbook.yaml file. The playbook does the following functions:
1. Tells Ansible to run the play on all hosts listed in your inventory file.
2. Tells ansible to use privilege escalation (usually sudo) to execute tasks that require elevated permissions.
3. Specifies the roles to be applied in the target hosts



