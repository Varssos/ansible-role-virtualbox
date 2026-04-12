# virtualbox

Ansible role to install [VirtualBox](https://www.virtualbox.org/) on Debian/Ubuntu systems.

## Requirements

- Debian or Ubuntu host
- `become: true` privileges (sudo)
- `ubuntu_codename` fact must be set (provided by `ubuntu-codename` role in pre_tasks)

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `virtualbox_package_name` | `virtualbox-7.1` | Package name to install via apt |
| `virtualbox_gpg_key_url` | `https://www.virtualbox.org/download/oracle_vbox_2016.asc` | URL to the GPG signing key |
| `virtualbox_gpg_keyring` | `/usr/share/keyrings/oracle-virtualbox-2016.gpg` | Path for the converted keyring file |

## Example Playbook

```yaml
- hosts: all
  become: true
  pre_tasks:
    - import_role:
        name: ubuntu-codename
  roles:
    - role: virtualbox
```

## License

MIT

## Author

Varssos