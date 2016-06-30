# Logs

ClawIO manages two main logs:

- The HTTP log stores HTTP requests in Apache-like format.
- The Application Log stores application events.

By default, ClawIO writes to `stdout` all the logs, as show below when running `clawiod` with no configuration:

```bash
./clawiod
INFO[0000] configuration detail                          confkey=server.base_url confval=/api/v1/ module=daemon
INFO[0000] configuration detail                          confkey=server.port confval=1502 module=daemon
INFO[0000] configuration detail                          confkey=server.jwt_secret confval=XXXXXXXXXXchange me module=daemon
INFO[0000] configuration detail                          confkey=server.jwt_signing_method confval=XXXXXXXXXX256 module=daemon
...
```

## HTTP Log

**Sample HTTP Logs**

```
INFO[0015] ::1 - - [30/Jun/2016:20:49:10 +0200] "OPTIONS /api/v1/metadata/list/ HTTP/1.1" 0 0 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari
INFO[0015] ::1 - - [30/Jun/2016:20:49:11 +0200] "POST /api/v1/metadata/init HTTP/1.1" 0 0 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari/537
INFO[0015] ::1 - - [30/Jun/2016:20:49:11 +0200] "GET /api/v1/metadata/list/ HTTP/1.1" 200 385 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari
```

The HTTP Log information is structured in [Combined Apache Log Format](http://httpd.apache.org/docs/2.4/logs.html#combined)

You can change the output for the HTTP log in the server configuration section:

```json
{
  "server": {

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
  }
}
```


**Application Log**

This log stores application events and assigns an unique Trace ID to every request so users' activity could be tracked through all the components in the ClawIO stack, thus becoming this log an important auditing piece.

ClawIO uses Logrus, a logging component that encourages careful, structured logging though logging fields instead of long, unparseable error messages. 
You could send this logs to log analyser service, like Logstash and browse them with Kibana for large deployments. 

**Sample app log from an ownCloud chunk upload**

```
INFO[0049] request started                               method=PUT module=server tid=7c16862f-75de-45e4-b99f-162558611402 uri=/api/v1/ocwebdav/remote.php/webdav/big-movie.avi-chunking-2818227562-265-264
INFO[0049] authenticated request                         module=server tid=7c16862f-75de-45e4-b99f-162558611402 user=demo
INFO[0049] upload is chunked                             module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0049] chunk info                                    chunk=&{pathSpec:big-movie.avi transferID:2818227562 totalChunks:265 currentChunk:264} module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk folder info                             chunkfolder=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk target info                             chunktarget=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/264 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] current amount of chunks                      chunk count=265 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] assembled file info                           assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/0 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/1 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/2 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/3 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/4 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/5 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/6 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/7 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0050] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/8 module=server tid=7c16862f-75de-45e4-b99f-162558611402

...

DEBU[0055] chunk appended to assembled file              assembledfile=/tmp/clawio-oc-chunks-temporary-namespace/294330163 chunk=/tmp/clawio-oc-chunks-temporary-namespace/chunking-2818227562-265/264 module=server tid=7c16862f-75de-45e4-b99f-162558611402
DEBU[0055] upload chunk to final destination             module=server pathspec=big-movie.avi tid=7c16862f-75de-45e4-b99f-162558611402
```


The application log can be configured in the server section:

```json
{
  "server": {

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
  }
}
```
