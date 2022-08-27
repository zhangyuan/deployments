# Airflow

## Install

```
helm install airflow ./ -n airflow --create-namespace
```

## Upgrade

```
helm upgrade airflow ./ -n airflow 
```

## Uninstall

```
helm uninstall airflow -n airflow 
```