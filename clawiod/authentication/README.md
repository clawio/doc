# Authentication configuration

ClawIO authentication can be controlled using one of the following
controllers:

- The [memory controller](memory.md) authenticates users against a list loaded from the configuration file.
- The [SQL controller](sql.md) authenticates users against a SQL database.

ClawIO uses the memory controller by default with one predefined user: `demo:demo`

These controllers do not support mutable operations (create, upate, delete) of users, they are just
read providers.

*We plan to develop more plugins for LDAP/AD, SAML and also mutable providers to manage users.* 

To change the authentication controller, specify the type you want to use
in the configuration file:

```json
{
 "authenticaton": {
    "type": "memory",
  },
}
```
