# OCSQL Storage

The ocsql storage interacts with the underlying local filesystem directly and has support
for ownCloud's metadata.

This storage also allows you to modify the filesystem with other tools and still being able to see the changes automatically.
The database will keep track of the FileID, ETag mtimes and checksums. All other metadata are obtained direclty from the filesystem.


To configure this storage you need to configure the data and metadata controllers for it.

## MetaData controller

```json
{
  "metadata": {
    "type": "ocsql",

    // the ocsql metadata controller obtains parts of the metadata
    // from the underlying local filesystem but it also stores ownCloud-related
    // metadata (ETAG, mtime, FileID) in a MySQL/MariaDB database.
    "ocsql": {

      // the path where user data will be stored
      "namespace": "/tmp/clawio-namespace",

      // the path where temporary data will be stored
      "temporary_namespace": "/tmp/clawio-temporary-namespace",

      // the connection configuration parameters for MySQL/MariaDB.
      "dsn": "",

      // the maximun number of idle connections between ClawIO and the SQL database
      "max_sql_idle_connections": 1024,

      // the maximun number of concurrent connections between ClawIO and the SQL database
      "max_sql_concurrent_connections": 1024,
      
      // where to store SQL queries.
      // Possible values: a file or "stdout"
      "sql_log": "stdout",

      // wheter or not to log SQL queries
      "sql_log_enabled": false,

      // if app_log is set to a file, the maximun file size in MiB for the file
      // before it gets rotated
      "sql_log_max_size": 100,

      // the maximum number of days to retain old log files based on the
      // timestamp encoded in their filename.  Note that a day is defined as 24
      // hours and may not exactly correspond to calendar days due to daylight
      // savings, leap seconds, etc. The default is not to remove old log files
      // based on age. 
      "sql_log_max_age": 0,

      // the maximum number of old log files to retain.  The default
      // is to retain all old log files (though sql_log_max_age may still
      // cause them to get deleted.)P
      "sql_log_max_backups": 0
    }
  }
}
```


## Data controller

```json
{
  "data": {
    "type": "ocsql",
    "upload_max_file_size": 8589934592,
    "ocsql": {
      // where to store user data. It must be same as the metadata controller.
      "namespace": "/tmp/clawio-namespace",

      // where to store temporary data
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
