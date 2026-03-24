# Ansible Role: ansible_role_swap

![Ansible](https://img.shields.io/badge/ansible-ready-blue.svg)
![Platform](https://img.shields.io/badge/platform-Ubuntu-lightgrey)
![License](https://img.shields.io/badge/license-Unlicense-green)

## Description

This Ansible role manages the creation and activation of a **Linux swap file**.  
It supports persistent configuration across reboots, allows control over system swappiness, and ensures a robust fallback mechanism if `fallocate` is unavailable.

### Features:
- Creates a swap file of configurable size
- Activates swap immediately and optionally adds it to `/etc/fstab`
- Adjusts `vm.swappiness` via `sysctl`
- Uses `fallocate` with optional fallback to `dd`

## Role Variables

The following variables can be set (see `defaults/main.yml`):

| Variable | Default | Description |
|----------|---------|-------------|
| `ansible_role_swap_file_path` | `/swapfile` | Filesystem path where the swap file will be created |
| `ansible_role_swap_file_size_mb` | `2048` | Size of the swap file in megabytes |
| `ansible_role_swap_swappiness` | `10` | Value for `vm.swappiness` (lower values reduce swap usage) |
| `ansible_role_swap_add_fstab` | `true` | If `true`, adds the swap file entry to `/etc/fstab` |
| `ansible_role_swap_activate` | `true` | If `true`, activates the swap file immediately via `swapon` |
| `ansible_role_swap_label` | `SWAPFILE` | Optional label assigned to the swap file (used by `mkswap -L`) |
| `ansible_role_swap_fallback_to_dd` | `true` | If `true`, uses `dd` if `fallocate` is not available |

## Usage Example

```yaml
- name: Configure swap on all hosts
  hosts: all
  become: true
  roles:
    - role: ansible_role_swap
```

## Sanity Checks

This role ensures:
- Swap file is created with the specified size and permissions
- It is registered in `/etc/fstab` if persistence is enabled
- System swappiness is adjusted via a persistent `sysctl` entry
- Uses `fallocate` when possible, falling back to `dd` if needed
- Activates the swap immediately if enabled

## License

Unlicense

## Author Information

Role maintained by Max Bergmann.  
