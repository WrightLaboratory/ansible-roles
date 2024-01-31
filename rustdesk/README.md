```bash
ansible-galaxy collection install -r requirements.yaml


export TARGET_FQDN='{{ fqdn_of_target_node }} | localhost'
export TARGET_USER='{{ local_account_with_sudo_on_target_node }}'

# To enable envsubst on Mac OS: `brew install gettext`
# Create inventory file

envsubst < inventory.yaml.template > inventory.yaml

# test connection to target node
ansible --user="${TARGET_USER}" -m ping -i inventory.yaml rustdesk
```
