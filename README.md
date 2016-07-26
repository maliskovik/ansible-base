# Base role

Every host should include this role.

## What it does?
* Sets hostname
* Sets locales
* Sets timezone
* Installs and configures monit
* Installs and configures ntp
* Installs and configures smart daemon to watch disk health status.
* Configures ssh
* Installs and configures UFW.
>Note: The UFW is restrictive y default, any role that configures a service to
use some new port, should also add a UFW rule.

* Adds the specified users and their SSH keys.

## Mandatory variables:

* admin_accounts - list containins names of admin-type user accounts to be created
> For each username specified, a directory with the same name must exist in the
`roles/base/files/users`. and must contain `.ssh/id_rsa.pub` file with the users public key.

* user_accounts - list containing names of normal user acounts to be created.
> Same requirements as with admin_accounts.


## Optional variables:

* admin_group - name of the admin groupe - default `sudo`
* base_locales - list of locales that should be present on the host.
* default_locale - default locale that should be used on the host. It must be
present in the base_locales list.
* admin_mails - list of admin email address that should recieve system mail.
* ntp_servers - list of ntp servers to be used.
