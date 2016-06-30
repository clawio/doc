# Hello World!

Welcome to the Hello World tutorial. In this short guide you will be able to : 

* Install and run the ClawIO Server Daemon (clawiod)
* Install the ClawIO Controller (clawioctl) to interact with clawiod from a terminal

## ClawIO Server Daemon

Download the [latest release of clawiod](https://github.com/clawio/clawiod/releases) for your platform, then extract and run it:

```bash
tar xvfz clawiod-*.tar.gz
cd clawiod-*
```

To start ClawIO, change to your clawiod build directory and run:

```bash
# By default, ClawIO stores data on your local filesystem
# at /tmp/clawio-namespace.
./clawiod 
```

ClawIO should start running and will expose metrics at [http://localhost:1502/metrics](http://localhost:1502/metrics)

## ClawIO Controller

Download the [latest release of clawioctl](https://github.com/clawio/clawioctl/releases) for your platform, then extract and run it:

```bash
tar xvfz clawioctl-*.tar.gz
cd clawioctl-*
```

To use the controller, change to your clawioctl build directory and run:

```bash
# By default, clawiod comes with an user called demo with password demo.
./clawioctl configure
Enter username (): demo
Enter password (******):
Enter authentication service base URL (http://localhost:1502/api/v1/authentication/):
Enter data service base URL (http://localhost:1502/api/v1/data/):
Enter metadata service base URL (http://localhost:1502/api/v1/metadata/):
Configuration saved to "/Users/labkode/.clawio/config"
```

Once the controller has been configured, we need to create our home directory.

```bash
./clawioctl metadata init
Home tree created!
```

Now we can list the contents of our home directory

```bash
./clawioctl metadata ls /
PATHSPEC  TYPE  SIZE MIMETYPE  CHECKSUM
```

At this point we do not have any data yet, so let's upload some files and create some folders

```bash
./clawioctl data upload ~/somefile.txt /somefile.txt
./clawioctl data upload ~/somefile.txt /somefile2.txt
./clawioctl data upload ~/somefile.txt /somefile3.txt
./clawioctl metadata mkdir /photos
./clawioctl data upload ~/myphoto.jpg /photos/myphoto.jpg
```

If we list again our home directory we will see the new added contents

```bash
./clawioctl metadata ls /
PATHSPEC       TYPE  SIZE  MIMETYPE                   CHECKSUM
photos         tree  102   clawio/tree
somefile.txt   blob  18    text/plain; charset=utf-8
somefile2.txt  blob  18    text/plain; charset=utf-8
somefile3.txt  blob  18    text/plain; charset=utf-8
```
