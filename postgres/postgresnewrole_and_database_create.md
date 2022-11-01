
# Ubantu postgres in create new database and role


- Here **vendingland** is database name
- Here **vendinguser** is role name **1234** is password 

**Note:** please makesure you are use in all smallcase

```bash
$ sudo su - postgres
$ psql
$ CREATE DATABASE vendingland;
$ CREATE USER vendinguser WITH PASSWORD '1234';
$ ALTER ROLE vendinguser SET client_encoding TO 'utf8';
$ ALTER ROLE vendinguser SET default_transaction_isolation TO 'read committed';
$ ALTER ROLE vendinguser SET timezone TO 'UTC';
$ GRANT ALL PRIVILEGES ON DATABASE vendingland TO vendinguser;
$ \q
$ exit

```
- here is the example set in setting file in django for postgres database
```bash
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql_psycopg2",
        "NAME": "vendingland",
        "USER": "vendinguser",
        "PASSWORD": "1234",
        "HOST": "localhost",
    }
}

```
