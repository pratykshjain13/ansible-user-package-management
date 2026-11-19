# Ansible User & Package Management Automation

## Project Overview

This project demonstrates Linux user management, group management, permission configuration, package installation, and service management across multiple RHEL-based Linux servers using Ansible.

The automation is performed from a centralized Ansible Control Node to multiple Managed Nodes using SSH connectivity and YAML playbooks.

## Architecture

- **Control Node:** RHEL Linux
- **Managed Nodes:** Two RHEL Linux servers
- **Automation Tool:** Ansible
- **Connection:** SSH key-based authentication
- **Package Manager:** YUM
- **Services Managed:** Apache HTTP Server (httpd)

## Project Features

### 1. User Management
- Create Linux users on multiple managed servers.
- Configure user home directories.
- Assign users to specific groups.

### 2. Group Management
- Create Linux groups.
- Add users to multiple groups.
- Manage primary and supplementary group membership.

### 3. Permission Management
- Create project directories.
- Configure directory ownership.
- Set Linux file and directory permissions.

### 4. Package Management
Automated installation of the following packages:

- Git
- Vim
- Curl

### 5. Service Management
- Stop Apache HTTP Server.
- Start Apache HTTP Server.
- Enable Apache service at system startup.
- Verify service status on managed nodes.

## Prerequisites

- One Ansible Control Node.
- Two or more RHEL-based Linux managed nodes.
- Ansible installed on the Control Node.
- Python installed on managed nodes.
- SSH connectivity between all nodes.
- Sufficient privileges for administrative tasks.

## Ansible Configuration

The project uses an `ansible.cfg` configuration file to define default settings.

Example:

```ini
[defaults]
inventory = ./inventory/hosts
remote_user = root
host_key_checking = False
```

Note: Disabling host key checking and using direct root SSH are intended only for this lab environment. Production environments should use secure host key verification and a dedicated sudo-enabled user.

## Inventory Configuration

Example inventory:

```ini
[webservers]
node1
node2
```

## Playbook Execution

### Verify Managed Node Connectivity

```bash
ansible all -m ping
```

### User and Group Management

```bash
ansible-playbook playbooks/user-management.yml
```

### Package Installation

```bash
ansible-playbook playbook/package-management.yml
```

### Stop Apache Service

```bash
ansible-playbook playbook/service-stop.yml
```

### Start Apache Service

```bash
ansible-playbook playbook/service-start.yml
```

### Verify Installed Packages

```bash
ansible webservers -m shell -a "git --version; vim --version | head -1; curl --version | head -1"
```

### Verify Apache Service

```bash
ansible webservers -m command -a "systemctl is-active httpd"
```

## Key Ansible Modules Used

| Module | Purpose |
|---|---|
| `user` | Create and manage Linux users |
| `group` | Create and manage Linux groups |
| `file` | Manage directories, ownership and permissions |
| `yum` | Install Linux packages |
| `service` | Start and stop services |
| `command` | Execute verification commands |
| `ping` | Verify Ansible connectivity |

## Skills Demonstrated

- Linux User and Group Administration
- Ansible Configuration Management
- YAML Playbook Development
- Inventory Management
- SSH Key-Based Authentication
- Package Management using YUM
- Linux Permissions and Ownership
- Apache Service Administration
- Multi-Server Automation

## Project Outcome

Successfully automated user creation, group management, directory permissions, package installation, and Apache service management across two RHEL managed nodes using Ansible.

This project demonstrates centralized Linux administration and repeatable configuration management through Ansible playbooks.
