# Yale Wright Laboratory Ansible Roles

## Introduction

These Ansible roles were developed to configure and maintain Redhat Enterprise Linux 8 (and their compatible distributions AlmaLinux 8, Rocky Linux 8, etc.) servers and their hosted applications at the [Yale Wright Laboratory](https://wlab.yale.edu).

While some workloads may be specific to the Wright Laboratory (eg, DocDB), the roles may easily be modified for similar workloads.
Of particular interest is the `podman-systemd` role for configuring servers to use rootless containers under [Podman](https://podman.io/).

These roles were developed and tested against AlmaLinux 8 instances hosted in AWS EC2 managed through Yale [Spinup](https://spinup.yalepages.org/).

## Pre-Requisites

1. Operating System: Linux, MacOS
2. Development Tools: Git, Pyenv, Python
3. Ansible

## Example: Setup an AlmaLinux 8 Instance to Host Rootless Container Under Systemd

This example uses the `almalinux-8-base` and `podman-systemd` roles to setup and update an AlmaLinux 8 instance, create a non-privileged user account, configure the non-privileged user account to linger through reboot cycles, and to prepare Systemd under the user's scope to enable hosting applications defined as Podman Systemd units.

On a management node, install Pyenv.
Install Python (~3) via Pyenv.

Create a directory for the Ansible playbook and change into that directory:

```bash
mkdir demo
cd demo
```

Create a new Python virtual environment:

```bash
python -m venv ./.venv
```

Activate the virtual environment:

```bash
source ./.venv/bin/activate
```

Create the `demo` playbook:

```bash
tee main.yml<<'_EOF'

_EOF
```

Initialize a git repository and commit `main.yml`

```bash
git init

git add main.yml
git commit -m 'Initial commit'
```

Add this repository as a submodule.

```bash
git submodule add roles
```
