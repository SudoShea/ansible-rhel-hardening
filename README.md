# Ansible System Hardening Playbook 🛡️

![Ansible Linting](https://github.com/SudoShea/ansible-system-hardening/actions/workflows/lint.yml/badge.svg)

An idempotent Ansible playbook and role designed to automate baseline security hardening for Linux servers, tailored for modern containerised homelab environments. Supports both **RedHat (RHEL/Fedora/Rocky/Alma)** and **Debian (Ubuntu/Debian)** distribution families.

---

## ⚡ Key Features

* **Cross-Family Compatibility:** Dynamically detects OS family to manage `firewalld` (RedHat) or `ufw` (Debian).
* **Homelab-Aware Baseline**: Preserves essential services like mDNS (`avahi-daemon`) and accommodates container networking (`ip_forward`, loose `rp_filter`, Podman bridge subnets).
* **Automated CI/CD Quality Control:** Fully validated on every push via `ansible-lint` and GitHub Actions workflows.
* **SSH & Authentication Hardening**: Enforces `PermitRootLogin no`, `PasswordAuthentication no`, tuned `MaxAuthTries`, and PAM session controls.
* **Built-in Tooling**: Includes automated dynamic version bumping (`scripts/bump_version.py`) and inventory-driven execution wrappers (`scripts/run.sh`).

---

## 📁 Repository Structure
```plaintest
├── CHANGELOG.md                   # Project change log adhering to Keep a Changelog
├── LICENSE                        # MIT License documentation
├── README.md                      # Project documentation and guide
├── VERSION                        # Single master source of truth for versioning
├── site.yml                       # Main playbook entrypoint
├── requirements.yml               # External Ansible collection dependencies
├── inventory.ini                  # Template inventory file for target mapping
├── inventory.local.ini            # Local override inventory (gitignored)
├── group_vars/
│   ├── all.yml                    # Local site overrides (gitignored)
│   └── all.yml.example            # Example group variables template
├── roles/
│   └── cis_hardening/             # Reusable core hardening role
│       ├── defaults/main.yml      # Safe baseline default variables
│       ├── handlers/main.yml      # System and service restart handlers
│       ├── tasks/                 # Modular CIS Level 1 task files
│       └── templates/             # Configuration templates (e.g., audit.rules.j2)
└── scripts/
    ├── bump_version.py            # Automated dynamic version synchronisation script
    └── run.sh                     # Inventory-driven playbook execution wrapper
```
---

## 📋 Requirements

* **Ansible Core:** `2.15+` installed on the control node.

## 🚀 Quick Start

### 1. Clone the repository & install dependencies
```bash
git clone https://github.com/SudoShea/ansible-system-hardening.git
cd ansible-system-hardening
ansible-galaxy collection install -r requirements.yml
```
### 2. Configure your inventory and environment overrides
Copy the template files to configure your local environment mappings:
* **Inventory Setup**:
```bash
cp inventory.ini inventory.local.ini
```
*(Edit `inventory.ini` to define your target node IP addresses and groups)*
* **Group Variables Setup (Optional)**:
```
cp group_vars/all.yml.example group_vars/all.yml
```
*(The core role provides secure baseline defaults in `roles/cis_hardening/defaults/main.yml`, but you can edit `group_vars/all.yml` to customise trusted subnets or operational parameters for your local environment.)*
### 3. Dry-Run Check
Use the execution wrapper to test execution across your nodes safely without applying changes:
```bash
./scripts/run.sh check
```
### 4. Apply Hardening
Execute the playbook live against a specific target or group using the wrapper:
```bash
./scripts/run.sh run <target_ip/group>
```
---
## 📄 License
Distributed under the MIT License. See `LICENSE` for details.
