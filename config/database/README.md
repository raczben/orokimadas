# PSQL configuration

Download the latest PSQL database: https://www.postgresql.org/download/
(It requires root privileges to install it.)

Use the pgAdmin tool.

Create a new user using the following script, by changing its password:

```sql
CREATE ROLE "adorApp" WITH
LOGIN
NOSUPERUSER
NOCREATEDB
NOCREATEROLE
INHERIT
NOREPLICATION
NOBYPASSRLS
CONNECTION LIMIT -1
PASSWORD '****';
```

Create a new database using the following script:

```sql
CREATE DATABASE adoration_db
WITH
OWNER = postgres
ENCODING = 'UTF8'
LOCALE_PROVIDER = 'libc'
CONNECTION LIMIT = -1
IS_TEMPLATE = False;
```

Then connect to the newly created `adoration_db` database and run the `db_script.sql` script to create the tables.
