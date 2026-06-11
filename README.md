# ansible-lemp-stack

Automated LEMP stack deployment on RHEL using Ansible.

Installs and configures **Nginx**, **MariaDB**, and **PHP-FPM** on any RHEL-based server in a single command.

---

## Stack

| Component | Package | Service |
|-----------|---------|---------|
| Web server | `nginx` | `nginx` |
| Database | `mariadb-server` | `mariadb` |
| PHP runtime | `php` + `php-fpm` | `php-fpm` |

---

## Requirements

- RHEL 10 / CentOS Stream 10 / AlmaLinux 10
- Ansible 2.14+
- SSH access to target servers
- sudo privileges on target servers

### Install Ansible

```bash
pip3 install ansible --user
```

---

## Usage

### 1. Clone the repository

```bash
git clone https://github.com/biroue10/ansible-lemp-stack.git
cd ansible-lemp-stack
```

### 2. Configure your inventory

Edit `inventory/hosts` and add your servers:

```ini
[lemp]
192.168.1.10
192.168.1.11
192.168.1.12
```

For local testing (same machine):

```ini
[lemp]
localhost ansible_connection=local
```

### 3. Run the playbook

```bash
ansible-playbook -i inventory/hosts playbook.yml --ask-become-pass
```

---

## Project Structure

```
ansible-lemp-stack/
├── inventory/
│   └── hosts              # Server inventory
├── roles/
│   ├── nginx/
│   │   └── tasks/
│   │       └── main.yml   # Install + start Nginx
│   ├── mariadb/
│   │   └── tasks/
│   │       └── main.yml   # Install + start MariaDB
│   └── php/
│       └── tasks/
│           └── main.yml   # Install PHP + PHP-FPM + start service
└── playbook.yml           # Main playbook
```

---

## Idempotent

Running the playbook multiple times is safe — Ansible only makes changes when the desired state differs from the current state.

```
PLAY RECAP
localhost : ok=7  changed=0  unreachable=0  failed=0
```

---

## Author

**Biroue Isaac** — [github.com/biroue10](https://github.com/biroue10)

Part of the [syseng-journey](https://github.com/biroue10/syseng-journey) project — Road to Senior Systems Engineer.
