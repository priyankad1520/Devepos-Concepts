# Ansible Full Concepts

Ansible is an open-source automation tool used for configuration management, application deployment, server provisioning, and task automation.

Ansible is developed by Red Hat.

Ansible helps DevOps Engineers automate repetitive infrastructure and server management tasks.

Ansible is agentless, it does not require installing agents on target servers.

Ansible mainly uses SSH for communication with Linux servers and WinRM for Windows servers.

Ansible uses YAML language for writing automation files called Playbooks.

## What is Configuration Management

Configuration Management is the process of maintaining systems in a consistent and desired state.

Configuration management automates software installation, updates, security settings, and server configurations.

Ansible helps manage infrastructure consistently across multiple servers.

## Why Ansible is Used

Ansible automates repetitive administrative tasks.

Ansible reduces manual server configuration work.

Ansible improves consistency across environments.

Ansible supports Infrastructure as Code practices.

Ansible integrates with cloud platforms, Docker, Kubernetes, and CI/CD pipelines.

Ansible simplifies application deployment and server management.

## Ansible Architecture

Ansible follows a simple controller-managed node architecture.

Main components are Control Node, Managed Nodes, Inventory, Modules, Playbooks, Roles, and Plugins.

### Control Node

Control Node is the system where Ansible is installed and executed.

The Control Node sends commands and configurations to managed servers.

### Managed Nodes

Managed Nodes are target servers managed by Ansible.

Managed Nodes do not require Ansible installation.

Managed Nodes require SSH access and Python installed for Linux automation.

### Inventory

Inventory file contains the list of managed servers.

Inventory groups servers logically for easier management.

Example inventory file:

```ini id="0s5r3m"
[web]
192.168.1.10
192.168.1.11

[db]
192.168.1.20
```

### Modules

Modules are reusable units used to perform automation tasks.

Modules handle package installation, file management, user management, service management, and cloud operations.

Common modules are `yum`, `apt`, `copy`, `service`, `user`, and `file`.

### Playbooks

Playbooks are YAML files containing automation tasks.

Playbooks define step-by-step infrastructure automation workflows.

### Roles

Roles organize playbooks into reusable structures.

Roles improve scalability and maintainability of automation code.

### Plugins

Plugins extend Ansible functionality.

Plugins support logging, connections, callbacks, and integrations.

## Ansible Installation

Install Ansible on Ubuntu:

```bash id="pjlwm7"
sudo apt update
sudo apt install ansible -y
```

Check Ansible version:

```bash id="lwz6b2"
ansible --version
```

## SSH Configuration

Ansible mainly communicates using SSH.

Generate SSH key:

```bash id="0qg9rf"
ssh-keygen
```

Copy SSH key to managed node:

```bash id="1jrm69"
ssh-copy-id user@server-ip
```

Test SSH connection:

```bash id="msm5zk"
ssh user@server-ip
```

## Ansible Inventory

Inventory defines target servers managed by Ansible.

Default inventory file location:

```text id="q5fr7z"
/etc/ansible/hosts
```

Check inventory hosts:

```bash id="b5v04n"
ansible all --list-hosts
```

## Ansible Ad-Hoc Commands

Ad-hoc commands execute single automation tasks quickly.

Ping managed nodes:

```bash id="mk4k9p"
ansible all -m ping
```

Check disk usage:

```bash id="9tw9v7"
ansible all -a "df -h"
```

Install package using apt module:

```bash id="aj7j7e"
ansible all -m apt -a "name=nginx state=present" --become
```

Restart service:

```bash id="3xq44v"
ansible all -m service -a "name=nginx state=restarted" --become
```

## Ansible Playbooks

Playbooks automate multiple tasks in sequence.

Playbooks use YAML syntax.

Basic playbook example:

```yaml id="d64r7j"
---
- hosts: web
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
```

Run playbook:

```bash id="t7mjlwm"
ansible-playbook nginx.yml
```

## YAML Basics

YAML is a human-readable configuration language.

YAML uses indentation instead of brackets.

YAML is widely used in Ansible, Kubernetes, and CI/CD tools.

## Important Ansible Modules

### Package Module

Installs packages on Linux systems.

Example:

```yaml id="3dcl3d"
apt:
  name: git
  state: present
```

### Service Module

Manages Linux services.

Example:

```yaml id="ev9kqf"
service:
  name: nginx
  state: started
```

### Copy Module

Copies files to managed servers.

Example:

```yaml id="2dys4n"
copy:
  src: file.txt
  dest: /tmp/file.txt
```

### File Module

Manages file permissions and directories.

Example:

```yaml id="zx6fcd"
file:
  path: /data
  state: directory
```

### User Module

Manages Linux users.

Example:

```yaml id="a7c4v7"
user:
  name: devops
  state: present
```

## Variables in Ansible

Variables make playbooks reusable and dynamic.

Example variable:

```yaml id="jlwm8m"
vars:
  package_name: nginx
```

Use variable:

```yaml id="ltjlwm"
name: "{{ package_name }}"
```

## Ansible Facts

Facts are system information collected automatically from managed nodes.

Facts include IP address, hostname, memory, operating system, and CPU information.

View facts:

```bash id="qjlwm1"
ansible all -m setup
```

## Ansible Roles

Roles organize automation code into reusable structures.

Role structure contains tasks, handlers, templates, files, and variables.

Create role:

```bash id="jlwm9p"
ansible-galaxy init nginx-role
```

## Ansible Galaxy

Ansible Galaxy provides reusable community roles.

Official Galaxy site:

```text id="jlwm0z"
https://galaxy.ansible.com
```

Install Galaxy role:

```bash id="jlwm2f"
ansible-galaxy install geerlingguy.nginx
```

## Templates in Ansible

Templates use Jinja2 syntax for dynamic configuration generation.

Template example:

```jinja2 id="jlwm6n"
ServerName {{ inventory_hostname }}
```

Deploy template:

```yaml id="jlwm3v"
template:
  src: config.j2
  dest: /etc/app.conf
```

## Handlers in Ansible

Handlers execute tasks only when notified by other tasks.

Handlers are commonly used for service restarts.

Example handler:

```yaml id="jlwm5x"
handlers:
  - name: restart nginx
    service:
      name: nginx
      state: restarted
```

## Ansible Loops

Loops execute repetitive tasks efficiently.

Example loop:

```yaml id="jlwm1t"
- name: Install packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - docker.io
    - nginx
```

## Ansible Conditionals

Conditionals execute tasks based on conditions.

Example:

```yaml id="jlwm4u"
when: ansible_os_family == "Debian"
```

## Ansible Vault

Ansible Vault encrypts sensitive information like passwords and keys.

Create encrypted file:

```bash id="jlwm8r"
ansible-vault create secrets.yml
```

Edit encrypted file:

```bash id="jlwm7y"
ansible-vault edit secrets.yml
```

Run playbook with vault password:

```bash id="jlwm4o"
ansible-playbook site.yml --ask-vault-pass
```

## Ansible with Docker

Ansible can manage Docker containers.

Example Docker container task:

```yaml id="jlwm6d"
docker_container:
  name: nginx
  image: nginx
  state: started
```

## Ansible with Kubernetes

Ansible can manage Kubernetes resources.

Example Kubernetes deployment task:

```yaml id="jlwm3c"
k8s:
  state: present
  src: deployment.yaml
```

## Ansible with Cloud Platforms

Ansible supports AWS, Azure, and Google Cloud automation.

Ansible can create servers, networks, storage, and cloud services automatically.

## Ansible Security

Use SSH keys instead of passwords for secure access.

Encrypt sensitive data using Ansible Vault.

Restrict sudo permissions carefully.

Use least privilege access for automation tasks.

## Ansible Best Practices

Use roles for reusable automation code.

Keep playbooks modular and organized.

Store playbooks in Git repositories.

Use variables instead of hardcoded values.

Encrypt secrets using Ansible Vault.

Test playbooks before production deployment.

## Ansible Advantages

Ansible is simple and easy to learn.

Ansible is agentless and lightweight.

Ansible uses human-readable YAML syntax.

Ansible supports multi-platform automation.

Ansible integrates with DevOps and CI/CD tools.

Ansible improves infrastructure consistency and automation speed.

## Ansible Limitations

Large-scale automation may become slower because Ansible uses SSH sequentially.

Complex playbooks may become difficult to manage without proper structure.

Windows automation requires WinRM configuration.

## Ansible Workflow

DevOps Engineer writes Ansible playbooks.

Inventory file defines managed servers.

Ansible Control Node connects to servers using SSH.

Ansible executes modules and automation tasks.

Servers are configured automatically based on playbook definitions.

Applications, packages, services, and configurations are managed consistently across environments.
