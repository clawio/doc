# Memory Controller

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
