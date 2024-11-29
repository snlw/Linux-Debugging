# Description
A web application relies on the PostgreSQL 13 database present on this server. However, the connection to the database is not working. Your task is to identify and resolve the issue causing this connection failure. The application connects to a database named app1 with the user app1user and the password app1user

## Process
Error seems to be that the PSQL connection is rejecting the host.
```
admin@i-0a7877f3a83937275:~$ PGPASSWORD=app1user psql -h 127.0.0.1 -d app1 -U app1user -c '\q'
psql: error: FATAL:  pg_hba.conf rejects connection for host "127.0.0.1", user "app1user", database "app1", SSL on
FATAL:  pg_hba.conf rejects connection for host "127.0.0.1", user "app1user", database "app1", SSL off
```

Check `pg_hba.conf` file.
`sudo vim /etc/postgresql/13/main/pg_hba.conf`

The line here rejects connections for localhost.
`host all all reject`

Change `reject` to `trust`.

Restart Service
`admin@i-0458cfb19a00350c5:/etc/postgresql/13/main$ /etc/init.d/postgresql restart`
