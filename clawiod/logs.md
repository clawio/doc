# Logs

ClawIO manages two logs:

- HTTP Log: logs HTTP requests in Apache-like format.
- App Log: logs application data.

By default ClawIO logs to `stdout` all the logs as show below when running `clawiod` with no configuration:

```bash
./clawiod

...

INFO[0000] endpoint registered                           endpoint=/api/v1/ocwebdav/remote.php/webdav/{path:.*} method=GET module=server
INFO[0000] endpoint registered                           endpoint=/api/v1/ocwebdav/remote.php/webdav/{path:.*} method=LOCK module=server
INFO[0000] endpoint registered                           endpoint=/api/v1/ocwebdav/status.php method=GET module=server
INFO[0000] endpoint registered                           endpoint=/api/v1/ocwebdav/ocs/v1.php/cloud/capabilities method=GET module=server
INFO[0000] system signals enabled for capture: SIGINT, SIGTERM, SIGHUP and SIGQUIT  module=daemon
INFO[0000] server listens on port 1502                   module=server

...

INFO[0015] request started                               method=OPTIONS module=server tid=164ba80f-7c8e-44dd-a52d-bef4429c2ed7 uri=/api/v1/authentication/token
INFO[0015] request ended                                 module=server tid=164ba80f-7c8e-44dd-a52d-bef4429c2ed7
INFO[0015] ::1 - - [30/Jun/2016:20:49:10 +0200] "OPTIONS /api/v1/authentication/token HTTP/1.1" 0 0 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari/537.36"
INFO[0015] request started                               method=POST module=server tid=2073d996-99bc-411c-a43d-b1a3c2eda7b0 uri=/api/v1/authentication/token
INFO[0015] token generated                               module=server tid=2073d996-99bc-411c-a43d-b1a3c2eda7b0 user=demo
INFO[0015] request ended                                 module=server tid=2073d996-99bc-411c-a43d-b1a3c2eda7b0
INFO[0015] ::1 - - [30/Jun/2016:20:49:10 +0200] "POST /api/v1/authentication/token HTTP/1.1" 201 233 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari/537.36"

```

## HTTP Log

**Sample HTTP Logs**

```
INFO[0015] ::1 - - [30/Jun/2016:20:49:10 +0200] "OPTIONS /api/v1/metadata/list/ HTTP/1.1" 0 0 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari
INFO[0015] ::1 - - [30/Jun/2016:20:49:11 +0200] "POST /api/v1/metadata/init HTTP/1.1" 0 0 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari/537
INFO[0015] ::1 - - [30/Jun/2016:20:49:11 +0200] "GET /api/v1/metadata/list/ HTTP/1.1" 200 385 "http://localhost:4200/login" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/50.0.2661.94 Safari
```

The HTTP Log information is structured in [Combined Apache Log Format](http://httpd.apache.org/docs/2.4/logs.html#combined)

**Application Log**

ClawIO logs application data and assigns an unique ID to every request so usre activity can be tracked through all the components in the ClawIO stack, thus becoming the app log a valuable source for auditing.
ClawIO uses Logrus, a logging component that encourages careful, structured logging though logging fields instead of long, unparseable error messages. For example, instead of: log.Fatalf("Failed to send event %s to topic %s with key %d"), you should log the much more discoverable:
