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

* base_network_config: A list of interfaces
  - Interface:
    - name: name of interface
    - mode: static/dynamic
    - addresses - list of IP addresses in IP/NETMASK format (192.168.1.1/24)
    - routes: list of routes - this has replaced gateway
* base_nameservers: list of DNS servers
* base_nameserver_search: default domain to search

## Optional variables:
* user_accounts: list containing names of normal user acounts to be created.
> Same requirements as with admin_accounts.

* user_accounts_local: Additional list of users to create
* admin_accounts_local: Additional list of admins to use
* base_admin_group: name of the admin groupe - default `sudo`
* base_admin_mails: list of admin email address that should recieve system mail.
* base_default_locale: default locale that should be used on the host. It must be present in the base_locales list.
* base_locales: list of locales that should be present on the host.
* base_hostname: Hostname to use - users inventory hostname by default
* base_motd: Path to motd file to use - path is ansible-repo relative
* base_fstab: Path to fstab file to use
* base_optional_dependencies_arch: List of optional packages to install on arch system
* base_optional_dependencies_centos: List of optional packages to install on Redhat system
* base_optional_dependencies_ubuntu: List of optional packages to install on ubuntu system
* base_sftp_group: sftp user group to be created and used
* base_sftp_homedir: Sftp homedir. Sftp users homes reside within
* base_sftp_users: List of sftp users to create

* base_scripts_dir_dest: Target directory for custo scripts
* base_scripts_dir_src: Local dir where scripts are stored to be pushed to remote.
* postfix_aliases_file: path to postfix aliases file to use
* base_ntp_open_to_address: Lis of IP addresses permited to query ntp
* base_ntp_open: Should ntp exposed
* base_ntp_servers: list of ntp servers to be used.
* base_users_dirs: Path to the directory which contains homedirs for users with .ssh subdirectory containing the id_rsa.pub file.
* hostfile_entries: A list of ip, name keypairs that will be added to the hosts file.
* ssh_permit_root_login: con be "yes", "no" or "without-password"
* ssh_port: ssh port to use.
* timezone: Which timezone to use
* ufw_allowed_public_ports: Ports to open
* ufw_allowed_hosts: Allow all access from these hosts (list)
* ufw_allowed_public_ports: List of ports to allow access to (globally)
* ufw_allowed_local_ports: List of UFW entries - limited by IP and port
* base_ufw_policy: UFW policy (default is deny)
* base_ssh_port_open: Defaults to True. Should default allow for ssh/22 be added
* base_ufw_public_IPs: Empty tring allows all IPs (IPv4 and IPv6) use "0.0.0.0/0" to restrict to IPv4

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
ufw_allowed_public_ports:
- port: 80
  proto: "tcp"
- port: 443
  proto: "tcp"
ufw_allowed_local_ports:
- port: 5432
  proto: tcp
  from: 192.168.11.1

```
