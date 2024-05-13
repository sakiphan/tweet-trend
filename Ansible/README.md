# Ansible Playbook for Jenkins Master and Slave Setup

## Overview

These Ansible playbooks are used to install and configure the necessary software on Jenkins Master and Slave machines. The Jenkins Master machine runs Jenkins, while the Jenkins Slave machines are used to execute various tasks. This configuration includes the installation of Java, Jenkins, Maven, and Docker.

## Requirements

- **Ansible**: These playbooks use Ansible to perform the necessary installations on Jenkins Master and Slave machines. Ensure that Ansible is installed on your local machine.
- **SSH Access**: You must have SSH access to the Jenkins Master and Slave machines.
- **Necessary Permissions**: The user accounts must have the required sudo permissions.
- **SSH Key**: You need to have the SSH private key file (`devops-key.pem`) required for Ansible to access the machines.

## Configuration Details

### Jenkins Master Playbook

This playbook performs the following actions on the Jenkins Master machine:
- Adds the Jenkins key.
- Adds the Jenkins repository.
- Installs Java.
- Installs and starts Jenkins.
- Enables Jenkins to start at boot time.

### Jenkins Slave Playbook

This playbook performs the following actions on the Jenkins Slave machine:
- Updates the Ubuntu repositories and cache.
- Installs Java.
- Downloads and extracts Maven.
- Installs and starts Docker.
- Grants necessary permissions to the Docker socket.
- Enables Docker to start at boot time.

## Inventory File

Use the following inventory file to define the IP addresses and SSH connection details for the Jenkins Master and Slave machines:

```ini
[jenkins-master]
10.1.1.153
[jenkins-master:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/devops-key.pem

[jenkins-slave]
10.1.1.152
[jenkins-slave:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/devops-key.pem
```

## Run the Ansible playbooks:

```bash
ansible-playbook -i /path/to/hosts jenkins-master-playbook.yaml
ansible-playbook -i /path/to/hosts jenkins-slave-playbook.yaml
```

## Additional Information

These playbooks are intended to be used with EC2 instances created using Terraform. Ensure that your EC2 instances are correctly configured and accessible via SSH before running these playbooks.



