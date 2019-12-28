# Ansible - Jupyter
Setup a Jupyter notebook on any server within a miniconda environment

Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks such as continuous deployments or zero downtime rolling updates [(Redhat, 2019)][1]. This repository contains an Ansible playbook to setup a public serving Jupyter notebook within a miniconda environment. Miniconda provides (similar to virtualenv) a controlled Python environment. See `environment.yml` for the installed Python dependencies.

## Setup
1) Generate password for the Notebook server using `from notebook.auth import passwd; passwd()`. This should have the form of type:salt:hashed-password.
1) Create vault from `group_vars/all/main.yml`
  ```bash
  # Copy group_vars file
  cp group_vars/all/main.yml group_vars/all/vault.yml

  # Edit new group_vars file
  nano group_vars/all/vault.yml

  # Encrypt new group_vars file
  ansible-vault encrypt group_vars/all/vault.yml
  ```
1) (Optional) Save vault secret to `VAULT_SECRET` in the root of this repository. It is git ignored, and you won't have to type it again.
1) Adjust `hosts.yml` with your target public IPs
1) Run `./run-playbook`


The notebook server is implemented as systemd service. If you ever require to view the logging, run `journalctl -eu jupyter.service`.

[1]: https://docs.ansible.com/ansible/latest/index.html