# Server Configuration

The server by default uses a poor secret to protect your credentials, you **MUST** change 
it ClawIO is going to be used by various people or if it is going to be public accessible from the internet.

Create a configuration file that contains at least the following information,
we will call it `clawiod.conf`:

```json
{
  ...

  "server": {
    "jwt_secret": "<your secret token>",
    "http_access_log": "<your file to store http logs>",
    "app_log": "<your file to store app logs>",
  },

  ...
}

```json
  "authenticaton": {
    "memory": {
      "users": [
        {
          "display_name": "<your display name>",
          "email": "<your email>",
          "password": "<your password>",
          "username": "<your username>"
        }
      ]
    },
  },

  "metadata": {
    "simple": {
      "namespace": "<your path where data will be stored>",
      "temporary_namespace": "<your path to store temporary data>"
    },
  },


  "data": {
    "simple": {
      "namespace": "<same as metadata simple namespace>",
      "temporary_namespace": "<same as metadata temporary_namespace>"
    },
  },
}
```
