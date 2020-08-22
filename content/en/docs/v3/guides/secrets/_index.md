---
title: Secrets
linktitle: Secrets
description: Setting up the secrets for your installation
weight: 30
---

Jenkins X 3.x uses [Kubernetes External Secrets](https://github.com/godaddy/kubernetes-external-secrets) to manage populating secrets from your underlying secret store such as:

* Alibaba Cloud KMS Secret Manager
* Amazon Secret Manager
* Azure Key Vault
* Hashicorp Vault
* GCP Secret Manager

This lets you check in all of your other kubernetes resources and custom resource definitions into git for simple and powerful GitOps.

You can then rotate secrets easily independent of git.

## Vault

If you are using Vault as your back end for [Kubernetes External Secrets](https://github.com/godaddy/kubernetes-external-secrets)  then before you try any of the following commands to populate secrets you need to make sure your termminal can access Vault.

To do this you can run the [jx secret vault portforward](https://github.com/jenkins-x/jx-secret/blob/master/docs/cmd/jx-secret_vault_portforward.md) command in a terminal. You should then be able to run the following `jx secret edit` or `jx secret import` commands.

## Edit Secrets

To edit the Secrets run:

```bash
jx secret edit
```                  

This will prompt you to enter all the missing Secrets by default.

If you just want to enter a specific secret you can use `--filter` or `-f` to filter for a specific secret name.

e.g.

```bash
jx secret edit -f nexus
```                  


## Export Secrets

You can export the current secrets to the file system via

```bash
jx secret export -f /tmp/mysecrets.yaml
```                  

Or to view them on the terminal...

```bash
jx secret export -c
```                  


## Import Secrets

If you have previously exported the secrets as shown above you can re-import them again (maybe into a different cluster):

```bash
jx secret import -f /tmp/mysecrets.yaml 
```                  


### Migrating Local Secrets

If you have booted Jenkins X before you may well have secrets in your `~/.jx/localSecrets/mycluster/secrets.yaml`

If the file is valid you can just run:

```bash
jx secret import -f ~/.jx/localSecrets/mycluster/secrets.yaml 
```                  

### Migrating Secrets from Vault

If you have secrets already in a Vault then use the vault CLI tool to export the secrets to disk, reformat it in the above YAML layout and then import the secrets as above.
