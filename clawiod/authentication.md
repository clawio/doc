# Authentication configuration

ClawIO default configuration comes with a demo user whose username is demo and password is demo.

ClawIO can be configured to authenticate users agains a variety of authentication providers thanks to its flexible design.

The current supported providers are:

- memory: users are defined on the configuration file. 
- sql: users are authenticated against a sql db (mysql or postgres)

These providers does not support mutable operations (create, upate, delete) over users, they are just
read providers.

*We plan to develop more plugins for LDAP/AD, SAML and also mutable providers to manage users.* 

To change the authentication controller, specify the type you want to use:

```json
{
 "authenticaton": {
    "type": "memory",
  },
}
```

## Memory Controller

When using this controller users are authenticated against the in-memory array of users defined in 
the configuration file.


```json
 "authenticaton": {
    "type": "memory",
    "memory": {
      "users": [
        {
          "display_name": "Demo User",
          "email": "demo@example.com",
          "password": "demo",
          "username": "demo"
        },
        {
          "display_name": "Jon Snow",
          "email": "jon@example.com",
          "password": "bastard",
          "username": "snow"
        }
      ]
    },
```

## SQL Controller
When using this controller users are authenticated against a MySQL or Postgres database.

```json
"authenticaton": {
    "type": "memory",
    "sql": {
      "driver": "mysql",
      "dsn": "root:passwd@tcp(localhost:3306)/users"
    }
  },
```

**It is required that you have created the DB on the chosen DB before starting the server. Tables will be created by the server on startup**
