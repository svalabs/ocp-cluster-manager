OpenShift Cluster Manager
=========================

## Preparation

### Install required software
```bash
yum install ansible python2-openshift
ansible-galaxy collection install -r requirements.yml
```

### Configuration files

This project allows reusing configurations for deployment of multiple OpenShift clusters.

Cluster-independent configuration is specified in `cluster/default.yml`.
Cluster-specific configuration is specified in YAML-files in `cluster/` directory, e.g. for "DEV" cluster there should be a file `cluster/dev.yml`.

### Setting up secrets using Ansible Vault

Secret variables will be stored in file `ansible/vars/ocp-secrets.yml`.
This file shall be encrypted by *ansible-vault* using an encryption password supplied in the file `ansible/vault_password`.

Use this script to create the `vault_password` and edit the encrypted secret file:

```bash
PASSWORD_FILE=$PWD/vault_password
SECRET_FILE=$PWD/vars/ocp-secrets.yml

# create password file
[ ! -f "${PASSWORD_FILE}" ] && (openssl rand -base64 32 > $PASSWORD_FILE)
# create secret file from example
[ ! -f "${SECRET_FILE}" ] && ansible-vault encrypt --vault-password-file="${PASSWORD_FILE}" \
  "${SECRET_FILE}.example" --output "${SECRET_FILE}"

# edit the secret file in editor
ansible-vault edit --vault-password-file="${PASSWORD_FILE}" "${SECRET_FILE}"
```

## Usage

### Cluster deployment

To deploy the cluster defined in `cluster/dev.yml`, run:

```bash
ENV_NAME=dev
ansible-playbook --vault-password-file=vault_password deploy-cluster.yml -e env_name=$ENV_NAME
```

### Destroy a cluster

```bash
ENV_NAME=dev
ansible-playbook destroy-cluster.yml -e env_name=$ENV_NAME
```
