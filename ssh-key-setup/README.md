# Ansible Playbook for Secure User Setup

This Ansible playbook is designed to automate the setup of a secure user environment on a server.

## Overview

1. **Target and User Definition**
    - Targets machines labeled as "server".
    - Does not gather facts about the target machines.
    - Connects using the `root` user.

2. **User Input**
    - Prompts for a username (displayed) and a new account password (hidden).

3. **Tasks**
    - **Install `whois`**: Ensures the `mkpasswd` utility is present.
    - **Generate password hash**: Uses `mkpasswd` to create a SHA-512 hash of the provided password.
    - **Generate SSH key**: Locally generates an RSA SSH key pair.
    - **Add new user**: Adds a new user with:
        - Provided username and hashed password.
        - Default shell (`/bin/bash`).
        - Membership in the `sudo` group.
    - **Deploy SSH Key**: Adds the generated public SSH key to the new user's authorized keys.
    - **Disable Password Authentication**: Modifies the SSH server config to use only key-based authentication.
    - **Disable Root Login**: Prevents direct root login via SSH.
    - Triggers SSH service restart if configurations change.

4. **Handlers**
    - **Restart SSH**: Restarts the SSH service when notified.

## Purpose

The playbook enhances server security by setting up a new user with sudo privileges, enabling SSH key-based authentication for the user, and disabling password authentication and direct root login.

## Prerequisites

- You need a `host.ini` file, which defines your target machines. Example format:

```ini
[server]
192.168.178.10
192.168.178.11
192.168.178.12
```

## How to Use

To execute the playbook, navigate to its directory and run the following command:
```bash
ansible-playbook ssh-key.yaml -i host.ini --ask-become
```

This command will prompt you for a sudo password when required.

Make sure both the `ssh-key.yaml` playbook and `host.ini` files are in the same directory or provide the appropriate paths in the command.
