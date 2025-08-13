# Role Name

create-ansible-user

## Description

This role creates a user named `ansible` with passwordless `sudo` privileges and adds an authorized key for SSH access.

## Requirements

- SSH connection to the managed nodes must be established.
- It is recommended to use SSH key-based authentication and passwordless `sudo` for privilege escalation.
- An SSH public key file `~/.ssh/id_rsa.pub` must exist on the control node from where you are running the playbook, as it will be used for the `authorized_key` module.

## Role Variables

- `ansible_user_groups`: This variable determines the group to which the `ansible` user is added to grant `sudo` privileges. It is set automatically based on the OS family (`sudo` for Debian-based systems, `wheel` for RedHat-based systems).

  File: `vars/main.yml`
  ```yaml
  ---
  # vars file for create-ansible-user
  ansible_user_groups:
    - "{{ 'sudo' if ansible_os_family == 'Debian' else 'wheel' }}"
  ```

## Dependencies

This role has no dependencies on other roles.

## Example Playbook

Here is an example of how to use the `create-ansible-user` role in a playbook:

```yaml
---
- hosts: all
  roles:
    - create-ansible-user
```

## How to use

To execute the role, run the `ansible-playbook` command, specifying your inventory file and playbook.

For example, from the root directory of the project:

```bash
ansible-playbook -i hosts.ini playbook.yml
```
