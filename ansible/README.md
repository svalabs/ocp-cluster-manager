
## Setting up secrets using Ansible Vault

Secret variables will be stored in file `ansible/vars/ocp-secrets.yml`.
This file shall be encrypted by *ansible-vault* using an encryption password supplied in the file `ansible/vault_password`.

Use this script to create the `vault_password` and edit the encrypted secret file:

```bash
cd ansible/
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
