# Creating a Rootless MediaWiki Podman Pod as `systemd` Service

## Create Ansible Vault File

First, you must create the Ansible vault files that will be used to create the MySQL database needed by the MediaWiki pod.

The sections from [mysql-README.MD](./mysql-README.md) are reproduced below:

```
ansible-playbook -i localhost, --connection local mysql-ansible-secrets-generate.yml
```

Next, you must create the MediaWiki vault file:

```
ansible-playbook -i localhost, --connection local mediawiki-ansible-secrets-generate.yml
```

The default value for `mediawiki_admin_user` is `admin`.
If you would like to customize that, then add the `-e` option.

```
ansible-playbook -i localhost, --connection local \
    -e "mediawiki_admin_user={{ custom_admin_user_name }}" \
    mediawiki-ansible-secrets-generate.yml
```

Encrypt the secrets file

```
ansible-vault encrypt --vault-id $(id -un)@${HOME}/.ansible/vaultpassword ${HOME}/.ansible/mediawiki-secrets.yml 
```

## Nginx Reverse Proxy SSL

Copy gzipped file containing certificate and key generated from your SSL management workstation to this repository's top level directory.
Extract the key and certificate to `./roles/nginx-revers-proxy/files` directory

```
service_domain_name="{{ fqdn_of_server }}"
tar -xvf ${service_domain_name}.gz -C ./roles/nginx-reverse-proxy/files

## Execute Playbook

```
mediawiki_site_name={{ NameOfWiki }}

ansible-playbook --user="${TARGET_USER}" \
    --vault-id "$(id -un)@${HOME}/.ansible/vaultpassword" \
    -e "@${HOME}/.ansible/mysql-secrets.yml" \
    -e "@${HOME}/.ansible/mediawiki-secrets.yml" \
    -e "mediawiki_site_name=${mediawiki_site_name}" \
    -i "${TARGET_FQDN}", \
    mediawiki-main.yml
```