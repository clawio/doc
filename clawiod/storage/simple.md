# Simple Storage

The simple storage interacts with the underlying local filesystem directly, without having any intermediate component. 
This allows you to modify the filesystem with other tools and still being able to see the changes automatically.


To configure this storage you need to configure the data and metadata controllers for it.

## MetaData controller

```json
{
  "metadata": {
    "type": "simple",
    "simple": {
      ## Where to store user data
      "namespace": "/tmp/clawio-namespace",
      ## Where to store temporary data. Usually under /tmp/
      "temporary_namespace": "/tmp/clawio-temporary-namespace"
    }
  }
}
```


## Data controller

```json
{
  "data": {
    "type": "simple",
    "upload_max_file_size": 8589934592,
    "simple": {
      ## Where to store user data. Must be the same as the metadata controller.
      "namespace": "/tmp/clawio-namespace",
      "temporary_namespace": "/tmp/clawio-temporary-namespace",

      // what checksum to use in server side.
      // It only makes sense when verify_client_checksum is enabled
      // Possible values: "md5", "adler32", "sha1", "sha256"
      "checksum": "",
      
      // wheter or not to verify client checksums to avoid data corruption
      "verify_client_checksum": false,
    }
  }
}
```
