# Deployment 

Download the [latest release of webui](https://github.com/clawio/webui/releases/) and uncompress it:

```bash
tar xvfz webui-*.tar.gz
```

We will use NGINX as our web server so you must have it already installed.
Create the following NGINX configuration file as save it as `nginx.conf`:

```nginx
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /usr/share/nginx/html;
	index index.html;

	# whatever url we are putting in the url we redirect to the index.html
	location / {
		try_files $uri $uri/ /index.html;
	}
}
```

Then perform the following actions:

* Copy the `nginx.conf` file to `/etc/nginx/conf.d/default.conf`
* Copy the contents of the `webui-*` folder to `/usr/share/nginx/html/`
* Restart NGINX with `service nginx restart`

Go to http://localhost:80 and you should see the login page.

![](assets/login-page.png)

After entering your credentials, you will access the `Objects Application`:

![](assets/objects-page.png)
