# ClawIO API Version 1




## API Basics ##

All API calls must be authenticated with a valid ClawIO API key.

```bash
curl -H 'Authorization: Bearer <Token>' http://localhost:1502/api/v1/authentication/ping
```

The api key can be obtained from the authenticaton API. See the <a href="#quick-start">Quick Start</a> for details.

## API Errors

Each endpoint defines the meaning of the HTTP Status Codes.
As a general rule, a 400 error will contain a JSON body explaining the cause of the error:

```json
{
    "code": 4,
    "message": "user or password do not match"
}
```

## Quick Start

**Obtain an access token**

```bash
curl -X POST http://localhost:1502/api/v1/authentication/token --data '{"username":"demo", "password": "demo"}'
```

```json
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkaXNwbGF5X25hbWUiOiJEZW1vIFVzZXIiLCJlbWFpbCI6ImRlbW9AZXhhbXBsZS5jb20iLCJleHAiOjE0NjcyODAwOTI5OTk0NzI1NDUsInVzZXJuYW1lIjoiZGVtbyJ9.VzoDYMQ18_5sy3L2SY6iSPIx0YqpSxuoCF5VSS_6t4I"
}
```

**Ping**

```bash
curl  http://localhost:1502/api/v1/authentication/ping -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkaXNwbGF5X25hbWUiOiJEZW1vIFVzZXIiLCJlbWFpbCI6ImRlbW9AZXhhbXBsZS5jb20iLCJleHAiOjE0NjcyODAwOTI5OTk0NzI1NDUsInVzZXJuYW1lIjoiZGVtbyJ9.VzoDYMQ18_5sy3L2SY6iSPIx0YqpSxuoCF5VSS_6t4I'
```

```
pong
```

## Authentication API ##

### Obtain Access Token ###

**POST** http://localhost:1502/api/v1/authentication/token

**Body content**

```json
{
	"username": "<username>",
	"password": "<password>"
}
```

**Sample request**

```bash
curl -X POST http://localhost:1502/api/v1/authentication/token --data '{"username":"demo", "password": "demo"}'
```

**Sample response**

```json
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJkaXNwbGF5X25hbWUiOiJEZW1vIFVzZXIiLCJlbWFpbCI6ImRlbW9AZXhhbXBsZS5jb20iLCJleHAiOjE0NjcyODAwOTI5OTk0NzI1NDUsInVzZXJuYW1lIjoiZGVtbyJ9.VzoDYMQ18_5sy3L2SY6iSPIx0YqpSxuoCF5VSS_6t4I"
}
```

**Success**

Response code is 201

**Errors**

- 400: username or password invalid or user not found

### Ping with Token ###

**GET** http://localhost:1502/api/v1/authentication/ping

**Sample request**

```bash
curl -H 'Authorization: Bearer <Token>' http://localhost:1502/api/v1/authentication/ping
```

**Sample response**

```
pong
```

**Success**

Response code is 200

## MetaData API

### Initialize home directory

**POST** http://localhost:1502/api/v1/metadata/init

**Sample request**

```bash
curl http://localhost:1502/api/v1/metadata/init -H "Authorization: Bearer <Token>"
```

**Success**

Response code is 200


### Create a Tree

**POST** http://localhost:1502/api/v1/metadata/createtree/{pathspec}

**Path parameters**

- pathspec: where the tree will be created

**Sample request**

```bash
curl -X POST http://localhost:1502/api/v1/metadata/createtree/photos -H "Authorization: Bearer <Token>"
```

**Success**

Response code is 201

**Errors**

- 404: the path does not exist 

### Examine an object

**GET** http://localhost:1502/api/v1/metadata/examine/{pathspec}

**Path parameters**

- pathspec: the path to the object

**Sample request**

```bash
curl http://localhost:1502/api/v1/metadata/examine/song_of_fire.txt -H "Authorization: Bearer <Token>"
```

**Sample response**

```json
{
    "checksum": "",
    "extra": null,
    "mime_type": "text/plain; charset=utf-8",
    "mtime": 1467278292000000000,
    "pathspec": "song_of_fire.txt",
    "size": 1140,
    "type": "blob"
}
```

*the extra field in the json payload can be used by the metadata controller
implementation to include additional information, for example, the ownCloud
metadata controller includes the ID and Etag in this field*

**Success**

Response code is 200

**Errors**

- 404: the object does not exist

### List a tree

**GET** http://localhost:1502/api/v1/metadata/list/{pathspec}

**Path parameters**

- pathspec: the path to the file

**Sample request**

```bash
curl http://localhost:1502/api/v1/metadata/list/photos -H "Authorization: Bearer <Token>"
```

**Sample response**

```json
[
    {
        "checksum": "",
        "extra": null,
        "mime_type": "image/png",
        "mtime": 1467283021000000000,
        "pathspec": "photos/drados.png",
        "size": 193,
        "type": "blob"
    },
    {
        "checksum": "",
        "extra": null,
        "mime_type": "image/png",
        "mtime": 1467283014000000000,
        "pathspec": "photos/ourense.png",
        "size": 1283717,
        "type": "blob"
    }
]
```

**Success**

Response code is 200

**Errors**

- 400: the object is not a tree and cannot be listed
- 404: the object does not exist

### Delete an Object

**DELETE** http://localhost:1502/api/v1/metadata/delete/{pathspec}

**Path parameters**

- pathspec: the path to the object

**Sample request**

```bash
curl -X DELETE http://localhost:1502/api/v1/metadata/delete/photos -H "Authorization: Bearer <Token>"
```

**Success**

Response code is 204

### Move an Object

**POST** http://localhost:1502/api/v1/metadata/move/{pathspec}?target={targetpathspec}

**Path parameters**

- pathspec: the object to be moved

** Query parameters **

- target: the new pathspec for the object

**Sample request**

```bash
curl -X POST http://localhost:1502/api/v1/metadata/move/photos?target=old_photos -H "Authorization: Bearer <Token>"
```

**Success**

Response code is 200

**Errors**

- 404: the object to be moved does not exist
- 400: the object cannot be moved to target because:
	- you are trying to move an object of type blob to a tree or viceversa
	- if source and target are tree objects and target is not empty 

## Data API ###

### Upload a blob###

**PUT** http://localhost:1502/api/v1/data/upload/{pathspec}

**Path parameters**

- pathspec: the new path of the blob

**Body content**

The body is the raw binary content of the file

**Headers**

- Checksum: the checksum for the blob, for example: `md5:f3b2d851c50951f930588f9a4ea5db2c`

**Sample request**

```bash
curl -i -X PUT http://localhost:1502/api/v1/data/upload/clawio_rocks.txt --data-binary @clawio_rocks.txt -H "Authorization: Bearer <Token>"
```

**Success**

Response code is 201

**Errors**

- 400: the request does not contain a body
- 404: the path does not exist 
- 412: the checksum sent does not match the server computed checksum 
- 413: the body of the request is bigger than the allowed maximun upload file size

### Download a BLOB###

**GET** http://localhost:1502/api/v1/data/download/{pathspec}

**Path parameters**

- pathspec: the path to the blob

**Sample request**

```bash
curl http://localhost:1502/api/v1/data/download/clawio_rocks.txt -H "Authorization: Bearer <Token>" -o /tmp/clawio_rocks.txt
```

**Sample response**

The response body is the content of the blob

**Success**

Response code is 200

**Errors**

- 404: the path does not exist



## WebDAV API ##
* This API implements the WebDAV protocol.
* Connect to this API at: http://localhost:1502/api/v1/webdav/

## OCWebDAV API ##

* This API implements the ownCloud Synchronization WebDAV protocol.
* Connect with an ownCloud's sync client to: http://localhost:1502/api/v1/ocwebdav/
* This API is not enabled by default, you need to add "ocwebdav" to the list of `enabled_services` in the configuration file.
* This API only works with a data and metadata controller whose name starts with "oc", like "ocsql".
