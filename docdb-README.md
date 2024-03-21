```
ansible-playbook --user="${TARGET_USER}" \
    --vault-id "$(id -un)@${HOME}/.ansible/vaultpassword" \
    -e "@${HOME}/.ansible/docdb-ansible-secrets.yml" \
    -i "${TARGET_FQDN}", \
    docdb-main.yml
```