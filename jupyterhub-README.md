# Instructions for Running `jupyterhub-main.yaml` Playbook

## Setting Up Control Node to Create jupyterhub

```bash
ansible-playbook -i localhost, --connection local jupyterhub-ansible-secrets-generate.yaml
```

Answer the prompts

Use `vi` to edit  `${HOME}/.ansible/vaultpassword` and replace the line with your plaintext password.
(Be sure not to add a new line.)

Encrypt resulting the `${HOME}/.ansible/jupyterhub-secrets.yaml` file

```bash
ansible-vault encrypt --vault-id $(id -un)@${HOME}/.ansible/vaultpassword ${HOME}/.ansible/jupyterhub-secrets.yaml
```

## Running Playbook with Encrypted Ansible Variable File

```bash
ansible-playbook --user="${TARGET_USER}" \
    --vault-id "$(id -un)@${HOME}/.ansible/vaultpassword" \
    -e "@${HOME}/.ansible/jupyterhub-secrets.yaml" \
    -i "${TARGET_FQDN}", \
    "jupyterhub-main.yaml"
 ```
