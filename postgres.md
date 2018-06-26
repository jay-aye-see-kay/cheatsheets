# General
On Mac (w/homebrew) superuser is the user that installed it, but on linux the default superuser is a new user called `postgres`, so command line stuff should be prefixed with `sudo -u postgres`.

## basic cli commands
```bash
createuser <username>
createdb <dbname>
psql [database] [user]   # opens a shell
```

# basic sql commands

```sql
alter user <username> with encrypted password '<password>';
```

```sql
grant all privileges on database <dbname> to <username>;
```

```sql
CREATE TABLE <tablename> (
    id serial primary key,
    name varchar(20) NOT NULL,
    desc text NOT NULL,
    date_added timestamp default NULL
);
```

```sql
CREATE TABLE <tablename> (
    id serial primary key,
    name varchar(20) NOT NULL,
    desc text NOT NULL,
    date_added timestamp default NULL
);
```

# other sql commands
`\q` or `\quit`
`\l` or `\list` (databases)
`\c` or `\connect` (to a database)
`\dt` (list tables in current db)
`\?` (help)