# OVH VPS Provision with Ansible

Automated, secure, and reproducible provisioning for OVH VPS using Ansible

## Overview

This project provides a comprehensive set of Ansible playbooks and roles to **automate the provisioning, hardening, and configuration of an OVH VPS**. It covers the entire lifecycle from initial user bootstrap to advanced security, Docker installation, and system finalization. The goal is to ensure your VPS is secure, up-to-date, and ready for production or development use—with minimal manual intervention.

## Project Purpose

- **Automate**: Eliminate manual setup by automating every step with Ansible.
- **Harden**: Apply best-practice security measures (SSH hardening, firewall, fail2ban, etc.).
- **Modernize**: Set up Docker for containerized workloads.
- **Finalize**: Transition to a secure SSH authentication strategy.
- **Idempotent**: Safely re-run playbooks without unwanted side effects.

## Prerequisites

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed on your local machine
- Python installed on the VPS (usually pre-installed)
- SSH access to your VPS (initial root or user access)
- Properly configured **Ansible inventory** file with your VPS details
- SSH key(s) for provisioning

## Features

- **User Bootstrap**: Create and configure a non-root admin user for ongoing management
- **SSH Hardening**: Configure secure SSH settings, disable password/root login, enforce key-based auth
- **Firewall**: Set up and enable UFW (Uncomplicated Firewall) with strict rules
- **Fail2ban**: Protect against brute-force attacks with fail2ban
- **Automatic Updates**: Enable unattended security updates
- **Docker Installation**: Install and configure Docker (and Compose) for container workloads
- **Finalization**: Disable default ubuntu user
- **Idempotency**: All tasks are safe to re-run, making updates and maintenance easy

## Project Structure

```tree
.
├── site.yml              # Main Ansible playbook
├── inventory             # Your VPS hosts inventory file
├── group_vars/           # Group-wide variable definitions
├── roles/
│   ├── bootstrap/        # Initial user and basic setup
│   ├── security/         # SSH, firewall, fail2ban, updates
│   ├── docker/           # Docker and Compose installation
│   └── finalize/         # Final hardening and cleanup
```

## Usage

1. **Clone this repository:**

    ```bash
    git clone https://github.com/theunfamousq/ovh-vps-provision.git
    cd ovh-vps-provision
    ```

2. **Configure your inventory:**
    - Edit the `inventory` file and add your VPS host(s) (IP address, SSH user, etc.).

3. **Customize variables:**
    - Edit files in `group_vars/` (or create `host_vars/` as needed) to set passwords, usernames, SSH keys and Docker options.

4. **Run the playbook:**

    ```bash
    ansible-playbook -i inventory site.yml
    ```

5. **Use tags for targeted runs:**
    - You can rerun specific roles using tags, e.g.:

      ```bash
      ansible-playbook -i inventory site.yml --tags "docker"
      ```

## Development & Contributions

Contributions, bug reports, and suggestions are welcome! To contribute:

- Fork the repository and create a feature branch
- Follow existing code/role structure and best practices
- Submit a pull request with a clear description

If you find an issue or need help, please open a [GitHub Issue](https://github.com/theunfamousq/ovh-vps-provision/issues).

## License

This project is licensed under the [MIT License](LICENSE).

## Author

Quentin ROUSSEY
