```
ansible-playbook -i localhost, --connection local mediawiki-ansible-secrets-generate.yml
```

If you would like to change the database name or the database user used by MediaWiki application, invoke the playbook using the `-e` option.

```
ansible-playbook -i localhost, --connection local \
    -e "mysql_database={{ database_name }}" \
    -e "mysql_username_={{ accountname_of_user_for_mediawiki }}" \
    mediawiki-ansible-secrets-generate.yml
```

Encrypt secrets file

```
ansible-vault encrypt --vault-id $(id -un)@${HOME}/.ansible/vaultpassword ${HOME}/.ansible/mediawiki-secrets.yml
```

Run playbook

```
ansible-playbook --user="${TARGET_USER}" \
    --vault-id "$(id -un)@${HOME}/.ansible/vaultpassword" \
    -e "@${HOME}/.ansible/mediawiki-secrets.yml" \
    -i "${TARGET_FQDN}", \
    mediawiki-main.yml
```