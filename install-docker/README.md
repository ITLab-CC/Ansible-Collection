# README.md for `install-docker-ubuntu.yaml`

## Overview

This Ansible playbook script, named `install-docker-ubuntu.yaml`, is designed to automate the process of installing Docker on a system running Ubuntu. It handles the installation of necessary prerequisites, sets up the Docker repository, and then installs Docker and its related tools. It also ensures that the specified user is added to the Docker group, granting them permission to run Docker commands without `sudo`.

## How It Works

1. **Prerequisites Installation**: The script first ensures that `ca-certificates`, `curl`, and `gnupg` are installed, which are required for fetching and verifying Docker's GPG key.
2. **Keyring Directory Creation**: It creates the `/etc/apt/keyrings` directory to store Docker's GPG key.
3. **Docker GPG Key Addition**: The script fetches Docker's GPG key from the official URL and saves it in the keyrings directory.
4. **Set Read Permissions**: It sets the necessary read permissions on the Docker GPG key.
5. **Docker Repository Addition**: The script configures the Docker repository in the system's sources list.
6. **APT Cache Update**: It updates the APT package cache to recognize the newly added Docker repository.
7. **Docker Installation**: The script installs Docker along with its related tools, including `docker-compose` and various plugins.
8. **Add User to Docker Group**: Finally, it adds the specified user (prompted at runtime) to the Docker group.

## Prerequisites

- You need a `host.ini` file, which defines your target machines. Example format:

```ini
[server]
192.168.178.10
192.168.178.11
192.168.178.12
```

## How to Use

To execute the script:

1. Ensure you have Ansible installed on your machine.
2. Navigate to the directory containing the `install-docker-ubuntu.yaml` and `host.ini` files.
3. Run the following command:

```bash
ansible-playbook install-docker-ubuntu.yaml -i host.ini --ask-become
```

When prompted, enter your username. This user will be added to the Docker group, allowing you to run Docker commands without needing sudo.

Note: The --ask-become flag prompts you for the sudo password, which is necessary for tasks that require elevated privileges.

# Dependencies

- Ansible
- Ubuntu OS on the target machine

