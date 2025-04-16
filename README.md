# Ansible Role: ansible_role_swap

![Ansible](https://img.shields.io/badge/ansible-ready-blue.svg)
![Platform](https://img.shields.io/badge/platform-Linux-lightgrey)
![License](https://img.shields.io/badge/license-MIT-green)

## Description

This Ansible role creates and configures a **Linux swap file**.  
It is suitable for physical and virtual machines, especially minimal systems or cloud instances where swap is not enabled by default.

### Features:
- Creates a swap file of configurable size and location
- Ensures proper permissions and formatting
- Optionally adds swap to `/etc/fstab` for persistence
- Optionally activates swap immediately
- Sets the `vm.swappiness` kernel parameter

---

## Role Variables

| Variable              | Default Value | Description                                                             |
|-----------------------|---------------|-------------------------------------------------------------------------|
| `swap_file_path`      | `/swapfile`   | Full path to the swap file                                              |
| `swap_file_size_mb`   | `2048`        | Size of the swap file in megabytes                                     |
| `swap_swappiness`     | `10`          | Kernel parameter controlling swap aggressiveness (0–100)                |
| `swap_add_fstab`      | `true`        | Whether to add the swap file to `/etc/fstab`                           |
| `swap_activate`       | `true`        | Whether to activate swap immediately using `swapon`                    |

> **Important:**  
> Ensure the file system supports swap files (e.g., ext4, xfs with correct options).  
> Not all filesystems or environments (e.g., certain containers) support swap activation.

---

## Usage Example

```yaml
- name: Configure swap on all target nodes
  hosts: all
  become: true
  roles:
    - role: ansible_role_swap
