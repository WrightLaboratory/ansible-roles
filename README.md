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
