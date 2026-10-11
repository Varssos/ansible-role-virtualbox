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

## Manual setup (without Ansible)

Run on amd64 Debian/Ubuntu or Linux Mint. The repository must support the
selected codename and the role's default package version, `virtualbox-7.1`:

```bash
. /etc/os-release
ubuntu_codename="${UBUNTU_CODENAME:-$VERSION_CODENAME}"
sudo apt install curl gnupg
curl -fL https://download.virtualbox.org/virtualbox/debian/oracle_vbox_2016.asc -o /tmp/oracle_vbox_2016.asc
sudo gpg --dearmor --yes --output /usr/share/keyrings/oracle-virtualbox-2016.gpg /tmp/oracle_vbox_2016.asc
sudo chmod 0644 /usr/share/keyrings/oracle-virtualbox-2016.gpg
rm /tmp/oracle_vbox_2016.asc
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/oracle-virtualbox-2016.gpg] https://download.virtualbox.org/virtualbox/debian $ubuntu_codename contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
sudo apt update
sudo apt install virtualbox-7.1
sudo usermod -aG vboxusers "$(id -un)"
```

Log out and back in for group membership to take effect. The role does not
install the Extension Pack; its tasks are commented out.

## License

MIT

## Author

Varssos