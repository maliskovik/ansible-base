# Base role

Every host should include this role.

## Supported distributions
* Ubuntu
* Archlinux

## What it does?
* Sets hostname
* Sets locales
* Sets timezone
* Installs and configures ntp
* Installs and configures smart daemon to watch disk health status.
* Configures ssh
* Installs and configures UFW.
>Note: The UFW is restrictive by default, any role that configures a service to
use some new port, should also add an UFW rule.

* Adds the specified users and their SSH keys.

## Mandatory variables:

* admin_accounts - list containins names of admin-type user accounts to be created
> For each username specified, a directory with the same name must exist in the
location specified by the base_users_dirs variable. and must contain `.ssh/id_rsa.pub` file with the users public key.

## Optional variables:
* user_accounts: list containing names of normal user acounts to be created.
> Same requirements as with admin_accounts.

* base_admin_group: name of the admin groupe - default `sudo`
* base_locales: list of locales that should be present on the host.
* base_default_locale: default locale that should be used on the host. It must be
present in the base_locales list.
* base_admin_mails: list of admin email address that should recieve system mail.
* base_ntp_servers: list of ntp servers to be used.
* timezone: Which timezone to use
* hostfile_entries: A list of ip, name keypairs that will be added to the hosts file.
* ssh_port: ssh port to use.
* ssh_permit_root_login: con be "yes", "no" or "without-password"
* base_users_dirs: Path to the directory which contains homedirs for users with .ssh subdirectory containing the id_rsa.pub file.
* ufw_allowed_public_ports: Ports to open
* base_ntp_open: Should ntp exposed
* base_ntp_open_to_address: IP-s to be opened to

## Example variables

```
admin_accounts:
  - admin
user_accounts:
  - test
base_admin_group: "sudo"
base_locales:
  - en_US.UTF-8
base_default_locale: "en_US.UTF-8"
base_admin_mails:
  - test@example.com
base_ntp_servers:
  - 8.8.8.8
  - 8.8.4.4
timezone: "Europe/Berlin"
hostfile_entries:
  - ip: ""
    names:
      - ""
ssh_port: "45632"
ssh_permit_root_login: "no"

```
