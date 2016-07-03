# Configuration

This is the layout of the WebUI application:

```
.
├── assets
│   ├── images
│   │   ├── background-bd315f87c2f3ee23aee3395139990c33.jpg
│   │   ├── logo-white.svg
│   │   └── logo.svg
│   ├── themes
│   │   └── default
│   │       └── assets
│   │           ├── fonts
│   │           │   ├── icons.eot
│   │           │   ├── icons.svg
│   │           │   ├── icons.ttf
│   │           │   ├── icons.woff
│   │           │   └── icons.woff2
│   │           └── images
│   │               └── flags-9c74e172f87984c48ddf5c8108cabe67.png
│   ├── vendor-917cc519bee01f0d403cde9a86bf5c02.css
│   ├── vendor-965b21db0f16efaaf168dc16ac07fc22.js
│   ├── webui-1344ed06cd72da007e389a9abe92c498.css
│   └── webui-b92084de522c03c75474ec3cc71cd4e4.js
├── crossdomain.xml
├── index.html
└── robots.txt

```

The file that contains the configuration directives for this application is the
`index.html` file, specifically the `<meta name="webui/config/environment">` tag.

```bash
cat index.html

<!DOCTYPE html>
...
<meta name="webui/config/environment" content="%7B%22modulePrefix%22%3A%22webui%22%2C%22environment%22%3A%22production%22%2C%22baseURL%22%3A%22/%22%2C%22locationType%22%3A%22auto%22%2C%22EmberENV%22%3A%7B%22FEATURES%22%3A%7B%7D%7D%2C%22APP%22%3A%7B%22name%22%3A%22webui%22%2C%22version%22%3A%220.1.0+749e0d6e%22%7D%2C%22apis%22%3A%7B%22authBaseUrl%22%3A%22/api/v1/authentication/%22%2C%22metaDataBaseUrl%22%3A%22/api/v1/metadata/%22%2C%22dataBaseUrl%22%3A%22/api/v1/data/%22%7D%2C%22ember-simple-auth%22%3A%7B%22authorizer%22%3A%22authorizer%3Atoken%22%2C%22routeAfterAuthentication%22%3A%22admin.objects-list-home%22%2C%22routeIfAlreadyAuthenticated%22%3A%22admin.objects-list-home%22%7D%2C%22ember-simple-auth-token%22%3A%7B%22serverTokenEndpoint%22%3A%22/api/v1/authentication/token%22%2C%22identificationField%22%3A%22username%22%2C%22passwordField%22%3A%22password%22%2C%22tokenPropertyName%22%3A%22access_token%22%2C%22authorizationPrefix%22%3A%22Bearer%22%2C%22authorizationHeaderName%22%3A%22Authorization%22%2C%22headers%22%3A%7B%7D%7D%2C%22exportApplicationGlobal%22%3Afalse%7D" />
...
```

The value of this meta tag is URL encoded, so if you copy its content and paste
it in a service like [UrlDecode](http://urldecode.org/), you will get the a JSON map:

```json
{
    "APP": {
        ## the name of the application
        "name": "webui",
        ## the version of the application alonside its last commit
        "version": "0.1.0 749e0d6e"
    },
    
    ## You do not need to touch this
    "EmberENV": {
        "FEATURES": {}
    },

    ## the location where the APIs live. If your WebUI server and clawiod
    ## server  are not on the same machine, you must change it to the location of
    ## your clawiod server.
    ## Example: http://demo.clawio.com:1502/api/v1/authentication/
    "apis": {
        "authBaseUrl": "/api/v1/authentication/",
        "dataBaseUrl": "/api/v1/data/",
        "metaDataBaseUrl": "/api/v1/metadata/"
    },
    
    ## If the WebUI files are not in the root of your web server, you have to
    ## change the baseURL accordingly.
    ## Example: /clawio/
    "baseURL": "/",

    ## You do not need to touch this
    "ember-simple-auth": {
        "authorizer": "authorizer:token",
        "routeAfterAuthentication": "admin.objects-list-home",
        "routeIfAlreadyAuthenticated": "admin.objects-list-home"
    },

    ## You do not need to touch this
    "ember-simple-auth-token": {
        "authorizationHeaderName": "Authorization",
        "authorizationPrefix": "Bearer",
        "headers": {},
        "identificationField": "username",
        "passwordField": "password",
        "serverTokenEndpoint": "/api/v1/authentication/token",
        "tokenPropertyName": "access_token"
    },

    ## You do not need to touch this
    "environment": "production",
    "exportApplicationGlobal": false,
    "locationType": "auto",
    "modulePrefix": "webui"
}
```

If you modify its contents, remember to URLEncode it when overwriting the meta tag.
