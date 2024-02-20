# Creating an Nginx Reverse Proxy Using a Self-Signed Certfifcate with Bundled Chain

Copy gzipped file containing certificate and key generated from your SSL management workstation to this repository's top level directory.
Extract the key and certificate to `./roles/nginx-revers-proxy/files` directory

```
service_domain_name="{{ fqdn_of_server }}"
tar -xvf ${service_domain_name}.gz -C ./roles/nginx-reverse-proxy/files
```

Execute the playbook.

```
export TARGET_FQDN={{ fully_qualified_domainname_of_server }}
export TARGET_USER={{ name_of_account_on_target_with_sudo }}

ansible-playbook --user="${TARGET_USER}" \
    --vault-id "$(id -un)@${HOME}/.ansible/vaultpassword" \
    -i "${TARGET_FQDN}", \
    "nginx-reverse-proxy-main.yml"
```