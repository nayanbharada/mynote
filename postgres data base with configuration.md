
# Postgres database with psql

## 
start with cmd

```bash
   sudo -u postgres psql
```

- it return list of database
```bash
   postgres=# \l

```

- adminuser is role name & lh_ventures is role password

```bash
postgres=# create user adminuser with encrypted password 'lh_ventures';
CREATE ROLE
```
- lh_ventures database name

```bash
postgres=# create database lh_ventures;
CREATE DATABASE
```
- all privileges to db "lh_ventures" with role "adminuser"
```bash
postgres=# grant all privileges on database lh_ventures to adminuser;
GRANT
```
