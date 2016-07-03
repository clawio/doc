# SQL Controller

When using this controller users are authenticated against a MySQL or Postgres database.

```json
"authenticaton": {
    "type": "sql",
    "sql": {
      "driver": "mysql",
      "dsn": "root:my-secret-pw@tcp(localhost:3306)/users"
    }
  },
```

*It is required that the databse already exists. If you use Docker, it is as simple as running `docker run -e MYSQL_ROOT_PASSWORD=my-secret-pw -e MYSQL_DATABASE=owncloud -d -P mysql --character-set-server=utf8 --collation-server=utf8_general_ci`*
