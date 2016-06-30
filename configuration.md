# Configuration
ClawIO is built with a default configuration so it can be run without having to specify any configuration file. If you want to customize some parameters
you can pass an optional flag to specify your JSON configuration file.


```bash
./clawiod -config my.conf
```

You do not need to specify all the configuration options in your configuration file, just the ones you need, for example, if `my.conf` is:

```json
{
	"server": {
		"port": 5555
	}
}
```
just the port will be overwritten and the rest of options will load it defaults.

You can see what configuration is loaded running `clawiod -showconfig` or `clawiod -config my.conf --showconfig`.

## Configuration directives
These are the configuration directives of ClawIO using default values (`clawiod -showconfig`) :

```json
{

  /**********************************/
  /****** SERVER DIRECTIVES *********/
  /**********************************/

  "server": {

    // the amount of cpu to be used
    "cpu": "100%",

    // the base url to expose the server APIs
    "base_url": "/api/v1/",

    // the port the server listens
    "port": 1502,

     // the secret to sign the authentication token. You must change it
    "jwt_secret": "you must change me",
    
    // the signing mehtod to sign the token. Currently only HS256 is supported.
    "jwt_signing_method": "HS256",
    
    // where to log HTTP(S) requests in Apache-like format.
    // The possible values are: a file or "stdout"
    "http_access_log": "stdout",

    // if http_access_log is set to a file, the maximun file size in MiB for the file
    // before it gets rotated
    "http_access_log_max_size": 100,

    // the maximum number of days to retain old log files based on the
    // timestamp encoded in their filename.  Note that a day is defined as 24
    // hours and may not exactly correspond to calendar days due to daylight
    // savings, leap seconds, etc. The default is not to remove old log files
    // based on age. 
    "http_access_log_max_age": 0,

    // the maximum number of old log files to retain.  The default
    // is to retain all old log files (though http_access_log_max_age may still
    // cause them to get deleted.)
    "http_access_log_max_backups": 0,

    // where to store application logs.
    // The possible values are: a file or "stdout"
    "app_log": "stdout",

    // the logging level.
    // The possible values are: "panic", "fatal", "error", "warning", "info", "debug"
    "app_log_level": "info",

    // if app_log is set to a file, the maximun file size in MiB for the file
    // before it gets rotated
    "app_log_max_size": 100,

    // the maximum number of days to retain old log files based on the
    // timestamp encoded in their filename.  Note that a day is defined as 24
    // hours and may not exactly correspond to calendar days due to daylight
    // savings, leap seconds, etc. The default is not to remove old log files
    // based on age. 
    "app_log_max_age": 0,

    // the maximum number of old log files to retain.  The default
    // is to retain all old log files (though app_log_max_age may still
    // cause them to get deleted.)
    "app_log_max_backups": 0,

    // the number of seconds to wait for active requests before shutting 
    // down the server
    "shutdown_timeout": 10,

    // wheter or not to use HTTPS
    "tls_enabled": false,

    // the file that contains the TLS certificate
    "tls_certificate": "",

    // the file that contains the private key to use in TLS communications
    "tls_private_key": "",

    // ClawIO is exposes several APIs, you can choose what services get exposed or not
    "enabled_services": [
      "authentication",
      "metadata",
      "data",
      "webdav",
      "ocwebdav"
    ],

    // wheter or not to enable CORS
    // See https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS
    "cors_enabled": true,
    
    // the origins to trust, null means "*" (trust all origins)
    // the value must be an array: ["www.example.org", "wwww.example2.com"]
    "cors_access_control_allow_origin": null,
    
    // the HTTP verbs to allow
    "cors_access_control_allow_methods": [
      "GET",
      "POST",
      "HEAD",
      "PUT",
      "DELETE"
    ],
    

    // the headers to allow, "*" means all
    "cors_access_control_allow_headers": [
      "*"
    ],

    // what services are exposed through CORS. Only services that will be 
    // reached from a browser should be enabled.
    "cors_enabled_services": [
      "authentication",
      "metadata",
      "data"
    ]
  },

  /**************************************************/
  /****** AUTHENTICATION SERVICE DIRECTIVES *********/
  /**************************************************/

  "authenticaton": {

    // the base url to expose the authentication API
    "base_url": "/authentication/",
    
    // the authentication controller to use
    // Possible values: "memory" or "sql"
    "type": "memory",
    
    // directives to configure the authentication memory controller
    "memory": {

      // the users of the system
      "users": [
        {
          "display_name": "Demo User",
          "email": "demo@example.com",
          "password": "demo",
          "username": "demo"
        }
      ]
    },
    
    // directives to configure the authentication sql controller
    "sql": {
      
      // the driver to use to connect to the database.
      // Possible values are: "mysql" or "postgres"
      "driver": "mysql",

      // the connection configuration parameters.
      // They differ from driver to driver.
      // For mysql: "user:password@tcp(ip:port)/dbname?charset=utf8" 
      // For postgres: "host=myhost user=gorm dbname=gorm sslmode=disable password=mypassword"
      // See http://jinzhu.me/gorm/database.html#connecting-to-a-database
      "dsn": "root:passwd@tcp(localhost:3306)/users"
    }
  },

  /**************************************************/
  /****** METADATA SERVICE DIRECTIVES ***************/
  /**************************************************/

  "metadata": {
    // the base url to expose the metadata API
    "base_url": "/metadata/",
    
    // the metadata controller to use
    // Possible values are: "simple" or "ocsql"
    "type": "simple",
    
    // the simple metadata controller obtains all the metadata from the 
    // the underlying local filesystem
    "simple": {

      // the path where user data will be stored
      "namespace": "/tmp/clawio-namespace",

      // the path where temporary data will be stored
      "temporary_namespace": "/tmp/clawio-temporary-namespace"
    },
    
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
      "sql_log_enabled": true,

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
  },

  /**************************************************/
  /****** DATA SERVICE DIRECTIVES *******************/
  /**************************************************/

  "data": {
    // the base url to expose the data API
    "base_url": "/data/",
    
    // the data controller to use
    "type": "simple",

    // the maximun file size allowed to be uploaded. Defaults to 8GiB
    "upload_max_file_size": 8589934592,

    // the simple data controller stores data in a local filesystem
    "simple": {

      // where to store user data
      "namespace": "/tmp/clawio-namespace",

      // where to store temporary data
      "temporary_namespace": "/tmp/clawio-temporary-namespace",

      // what checksum to use in server side.
      // It only makes sense when verify_client_checksum is enabled
      // Possible values: "md5", "adler32", "sha1", "sha256"
      "checksum": "",
      
      // wheter or not to verify client checksums to avoid data corruption
      "verify_client_checksum": false,
    },
    "ocsql": {
      // where to store user data
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
  },

  /**************************************************/
  /****** WEBDAV SERVICE DIRECTIVES *****************/
  /**************************************************/

  "webdav": {

    // the base url to expose the WebDAV API
    "base_url": "/webdav/",

    // the maximun file size allowed to be uploaded. Defaults to 8GiB
    "upload_max_file_size": 8589934592,

    // the data controller to use 
    "data_controller": "simple",

    // the metadata controller to use 
    "meta_data_controller": "simple"
  },

  /**************************************************/
  /****** OCWEBDAV SERVICE DIRECTIVES ***************/
  /**************************************************/

  "ocwebdav": {

    // the base url to expose the ownCloud WebDAV Sync API
    "base_url": "/ocwebdav/",

    // the maximun file size allowed to be uploaded. Defaults to 8GiB
    "upload_max_file_size": 8589934592,

    // the data controller to use. It must be set to "ocsql"
    "data_controller": "ocsql",
    
    // the metadta controller to use. It must be set to "ocsql"
    "meta_data_controller": "ocsql",

    // where to store file chunks
    "chunks_namespace": "/tmp/clawio-oc-chunks-namespace",

    // where to store temporary file chunks
    "chunks_temporary_namespace": "/tmp/clawio-oc-chunks-temporary-namespace"
  }
}
```
