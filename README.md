# Ansible Playbook for EC2 Instance Setup
This repository provides an Ansible playbook to install required software and tools on AWS EC2 instances.

## Prerequisite
- **Ansible Installation:** Ensure [ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) is installed on your machine.
- **Private Keys:** Needed for EC2 access
    - JLeague instances private key: S3 bucket path application-resources-backup -> jleague -> ec2 private keys
    - Raven instances private key: S3 bucket path application-resources-backup -> raven -> ec2 private keys
    - Download and place keys in the `private_keys` directory and set permissions using the command `chmod 600 <key-file-name>`

## Folder Structure
```
.
|- .gitignore             # Git ignore patterns for untracked files
|- private_keys           # Directory for EC2 private keys
|- roles                  # Reusable Ansible components
    |- backend            # Installs dotnet, copies service file to manage app lifecycle
    |- codedeploy         # Installs CodeDeploy agent for CodePipeline
    |- letsencrypt        # Installs Certbot and obtains SSL certificates
    |- nginx              # Installs Nginx and copies configuration files
|- vars                   # Variables declarations
|- ansible.cfg            # Ansible configuration settings
|- hosts                  # Inventory file listing managed hosts
|- play.yaml              # Playbook with tasks for specified hosts/groups
|- README.md              # Repository overview and usage details
```

## Connectivity Test Commands
Test the connection for different environments as follows:
- `Development:` ansible -m ping dev
- `Staging:` ansible -m ping staging
- `Production:` ansible -m ping prod


## Usage
Run the playbook for different environments as follows:
- `Development:` ansible-playbook play.yaml -e env=dev
- `Staging:` ansible-playbook play.yaml -e env=staging
- `Production:` ansible-playbook play.yaml -e env=prod
