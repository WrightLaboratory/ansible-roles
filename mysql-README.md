```
ansible-playbook -i localhost, --connection local mysql-ansible-secrets-generate.yml
```

If you would like to change the database name or the database user used by MediaWiki application, invoke the playbook using the `-e` option.

```
ansible-playbook -i localhost, --connection local \
    -e "mysql_database={{ database_name }}" \
    -e "mysql_username_={{ accountname_of_user_for_mysql }}" \
    mysql-ansible-secrets-generate.yml
```

Encrypt secrets file

```
ansible-vault encrypt --vault-id $(id -un)@${HOME}/.ansible/vaultpassword ${HOME}/.ansible/mysql-secrets.yml
```

Run playbook

```
ansible-playbook --user="${TARGET_USER}" \
    --vault-id "$(id -un)@${HOME}/.ansible/vaultpassword" \
    -e "@${HOME}/.ansible/mysql-secrets.yml" \
    -i "${TARGET_FQDN}", \
    mysql-main.yml
```

This will create a user systemd service running under the context of service account named `mysql` on the target node.
This service will launch a rootless podman container running a MYSQL data base.
This service account `mysql` is enabled to linger past reboots.
The database files will be in the homedir of the service account in at the following path: `/var/lib/mysql/data/db`.
