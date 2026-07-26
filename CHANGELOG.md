# Changelog

All notable changes to the `ansible-system-hardening` project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.1] - 2026-07-26

### Fixed
- Correct `README.md` spelling in line with AU-English spelling

## [1.1.0] - 2026-07-26

### Added
* **Dedicated Version Tracker (`VERSION`)**: Implemented a clean, single-file version source of truth to streamline automated release management.
* **Dynamic Version Bumper (`scripts/bump-version.py`)**: Added a Python utility to automate semantic version increments against the `VERSION` file.
* **Execution Wrapper (`scripts/run.sh`)**: Added an inventory-driven shell script to streamline dry-runs (`--check --diff`) and targeted live playbook executions against local node definitions (`inventory.local.ini`).
* **Inventory Template (`inventory.ini`)**: Provided a clean template file designed to be copied locally for environment-specific node mapping.

### Changed
* **Decoupled Architecture**: Extracted homelab-specific networking parameters and operational overrides from the core role into `group_vars/all.yml` to keep the `cis_hardening` role fully sanitised and reusable.
* **Refactored Role Defaults**: Updated `roles/cis_hardening/defaults/main.yml` to hold strict, generic fallback defaults that are cleanly overridden by environment group variables.

## [1.0.1] - 2026-07-24
### Fixed
- Refactored `site.yml` tasks to replace `ignore_errors` with explicit `failed_when: false` handling.
- Corrected YAML syntax formatting and document markers in `site.yml`.

### Added
- Added `requirements.yml` to track external Ansible collection dependencies (`community.general` and `ansible.posix`).
- Integrated automated CI/CD pipeline using GitHub Actions and `ansible-lint`.

## [1.0.0] - 2026-05-10
### Added
- Initial release of automated system hardening and firewall management playbooks.
