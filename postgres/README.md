# PostgreSQL

## Install

```
helm install postgres ./ -n postgres --create-namespace
```

## Upgrade

```
helm upgrade postgres ./ -n postgres 
```

## Notes

### pg_hba.conf

The default `/var/lib/postgresql/data/pg_hba.conf` as below allows access to the database with no password when using `kubectl port-forward svc/postgres 5432:5432 --namespace postgres`:

```conf
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     trust
host    replication     all             127.0.0.1/32            trust
host    replication     all             ::1/128                 trust

host all all all md5
```

By settings `POSTGRES_INITDB_ARGS` as `--auth-host=scram-sha-256`. The conf becomes as below:

```conf
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     trust
host    replication     all             127.0.0.1/32            scram-sha-256
host    replication     all             ::1/128                 scram-sha-256

host all all all scram-sha-256
```

Changes made to `POSTGRES_INITDB_ARGS` only takes effect when init the database as the data folder is persistent.