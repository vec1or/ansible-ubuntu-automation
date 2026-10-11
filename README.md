# Ansible Ubuntu Server Automation

An Infrastructure as Code project that automates Ubuntu server configuration using Ansible.

## Overview

This project demonstrates automated server provisioning, package management, Nginx configuration, reusable roles, Jinja2 templates, handlers, and secrets management with Ansible Vault.

## Tech Stack

- Ansible
- Ubuntu Linux
- Nginx
- YAML
- Jinja2
- Ansible Vault

## Project Structure

```text
ansible-lab/
├── inventory.ini
├── playbook.yml
├── packages.yml
├── site.yml
├── nginx-role.yml
├── server-setup.yml
├── vault-demo.yml
├── roles/
│   └── nginx/
│       ├── defaults/
│       ├── handlers/
│       ├── meta/
│       ├── tasks/
│       ├── templates/
│       ├── tests/
│       └── vars/
└── templates/
    └── ansible-site.conf.j2
```

## Features

- Automated installation of system packages
- Nginx installation and configuration
- Website directory and permission management
- Creation of a Linux `webadmins` group
- Configuration using Jinja2 templates
- Reusable Ansible roles and handlers
- Secrets management demonstration with Ansible Vault

## Prerequisites

- Ubuntu Linux
- Ansible installed
- Sudo/root privileges

## Usage

**1. Verify the Ansible inventory**

```bash
ansible -i inventory.ini local -m ping
```

**2. Check the server configuration playbook**

```bash
ansible-playbook -i inventory.ini server-setup.yml --syntax-check
```

**3. Apply the configuration**

```bash
sudo ansible-playbook -i inventory.ini server-setup.yml
```

The playbook installs required packages, creates the `webadmins` group, deploys a sample website, and configures Nginx.

**4. Verify idempotency**

Run the playbook again:

```bash
sudo ansible-playbook -i inventory.ini server-setup.yml
```

Previously configured resources should generally report `ok` rather than `changed`.

## Ansible Vault

The `vault-demo.yml` playbook demonstrates loading an encrypted variable from `vault-lab/secrets.yml`.

Create a local Vault file:

```bash
mkdir -p vault-lab
ansible-vault create vault-lab/secrets.yml
```

Add a demonstration variable:

```yaml
demo_password: "replace-with-demo-value"
```

Run the demonstration:

```bash
ansible-playbook -i inventory.ini vault-demo.yml --ask-vault-pass
```

The Vault file is intentionally excluded from version control.

## Security Notes

- Do not commit Vault passwords or plaintext secrets.
- Review inventories before publishing real server addresses.
- Review playbooks before executing privileged operations.
- Use Vault and secure secret-management practices for production environments.

## Learning Outcomes

This project demonstrates repeatable Linux server configuration, configuration management, idempotency, reusable automation components, and infrastructure security fundamentals.
