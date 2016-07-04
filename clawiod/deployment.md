## Deployment 

Download the [latest release of clawiod](https://github.com/clawio/clawiod/releases/) for your platform, then extract and run it:

```bash
tar xvfz clawiod-*.tar.gz
cd clawiod-*
```

To start the server, change to your clawiod build directory and run:

```bash
./clawiod
```

The daemon should start listening on port 1502.

*We are working on init scripts so it will be much easy in the future to run the service*


The server runs with a default configuration: the user is demo, password is demo  and data is stored on `/tmp`.
If you are just playing with ClawIO it's fine to leave it like that, else you must specify the server secret token. You can use a passphrase
or better, generate it randomly.

When you have your secret create a [configuration file](../configuration) with the following content:

```json
{
  "server": {
    "jwt_secret": "<your really hard to guess secret token>",
  }
}
```

Once clawiod is up and running you can interact with it issuing raw curl commands to the [API](../api) or use the following clients:

- [ClawIO Terminal Controller](../clawioctl/README.md)
- [ClawIO Web UI](../webui/README.md)
- [ownCloud Sync clients](https://owncloud.org/install/#install-clients)
- Generic WebDAV Clients like [CyberDuck](https://cyberduck.io/) or built-in clients like [Finder in MacOS](https://support.apple.com/kb/ph18514?locale=en_US).



