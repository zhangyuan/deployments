# Vault

## Install

```
helm dependency build
helm install vault ./ -n vault --create-namespace
```

## Upgrade

```
helm upgrade vault ./ -n vault 
```