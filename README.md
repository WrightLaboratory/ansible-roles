# Ansible Playbooks

This is a collection of playbooks to setup various servers at the Wright Lab.

## Pre-requesites

`pyenv` should have been configured for the managment node or localhost if running playbooks locally.

```bash
pyenv install $(cat .python-version)

python -mvenv .venv

source ./.venv/bin/activate

pip install -r requirements.txt
```

```bash
# Install ansible playbook requirements
ansible-galaxy collection install -r requirements.yaml

# Create new roles for use in subsequent toplevel main-*.yaml files
ansible-galaxy role init --offline --init-path ./roles "{{ role_name }}"
```

Execute playbook

```bash
export TARGET_FQDN='{{ fqdn_of_target_node }} | localhost'
export TARGET_USER='{{ local_account_with_sudo_on_target_node }}'

# test ping using adhoc command
ansible "${TARGET_FQDN}" --user="${TARGET_USER}"  -m ping -i "${TARGET_FQDN}",

# run playbook
ansible-playbook --user="${TARGET_USER}" -i "${TARGET_FQDN}", "main-{{ name_of_app }}.yaml"
```