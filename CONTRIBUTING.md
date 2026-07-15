# Contributing to Forks Life Node

## Overview

This repository contains automated deployment scripts for the Forks Life Wallet on Linux-based infrastructure. It represents the first operational implementation of the ixBase ecosystem's multi-currency wallet deployment and management framework.

## Repository Structure

```
.
├── install.sh           # Automated deployment script
├── README.md            # Installation guide & configuration
├── LICENSE              # MIT License
├── CONTRIBUTING.md      # This file
└── .gitignore           # Git exclusions
```

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/forks-ecosystem/forks-life-node.git
   cd forks-life-node
   ```

2. **Review the README** for installation instructions

3. **Test on a clean Ubuntu/Debian system** before deploying to production

## Security Considerations

When modifying the installer or configuration:

### Privilege Escalation
- Minimize use of `sudo`. Every privilege elevation should be documented and justified.
- Never request `NOPASSWD: ALL` — only grant specific commands.
- Use `/etc/sudoers.d/` for managing sudo rules (never edit `/etc/sudoers` directly).

### File Permissions
- Web-accessible directories must have restricted permissions (644 for files, 755 for directories)
- Database and credential storage directories must be 700 (rwx------)
- Credentials file must be 640 (rw-r-----)

### Credential Storage
- Sensitive data is stored in `/var/www/utx/credentials.env` with restricted access
- Never hardcode credentials in the script
- Always use environment variables or secure configuration files

### Service Management
- sudo rules for systemctl commands must be explicit and limited
- Example: `www-data ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx` (good)
- Example: `www-data ALL=(ALL) NOPASSWD: /usr/bin/systemctl *` (bad)

## Testing Checklist

Before submitting changes, test on a clean system:

- [ ] NGINX installs and configures correctly
- [ ] PHP-FPM starts and processes PHP scripts
- [ ] SQLite3 database files are created with proper permissions (600)
- [ ] Web-accessible directories have 755 permissions
- [ ] Credential file is not world-readable (640)
- [ ] Service restart capabilities work with appropriate sudo rules
- [ ] All symlinks are created correctly
- [ ] No hardcoded paths that won't work on different systems
- [ ] Script is idempotent (can be run multiple times safely)

## Code Style

- Use `#!/bin/bash` shebang
- Use `set -e` to exit on errors
- Quote all variables: `"$variable"` not `$variable`
- Use descriptive variable names
- Add emoji prefixes for readability (🛠, 📦, etc.)
- Comment complex logic

## Future Enhancements

This module will evolve to incorporate:

- Advanced formalization layers from [ixBase SPEC](https://github.com/forks-ecosystem/ixbase/blob/main/docs/SPEC.md)
- Cross-cultural barrier normalization for multi-region deployments
- Polyglot database topology for archival integrity
- Enhanced security frameworks aligned with ixBase architectural axioms
- Support for additional Linux distributions and architectures

## Relationship to ixBase

This repository implements the operational layer of the ixBase ecosystem:

- **ixBase/docs/SPEC.md**: Architectural specification
- **ixBase/design/ui-responsiveness**: Reflected in fast wallet deployment
- **ixBase/design/database-topology**: SQLite as polyglot-compatible storage
- **ixBase/design/cultural-barriers**: Multi-currency support (BTM, BRI, GOR, etc.)

## Questions & Discussion

For questions about ixBase architecture, refer to:
- Main ixBase repository: https://github.com/forks-ecosystem/ixbase
- ixBase Specification: https://github.com/forks-ecosystem/ixbase/blob/main/docs/SPEC.md

## License

This project is licensed under the MIT License — see the LICENSE file for details.
