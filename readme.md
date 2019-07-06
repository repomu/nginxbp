[![](https://img.shields.io/badge/nginx-1.17.1-009688.svg)](https://nginx.org/) [![](https://img.shields.io/badge/openssl-1.1.1c-009688.svg)](https://www.openssl.org/) [![](https://img.shields.io/badge/zlib-1.2.11-009688.svg)](https://www.zlib.net/) [![](https://img.shields.io/badge/pcre-8.43-009688.svg)](https://www.pcre.org/) [![](https://img.shields.io/badge/head--more-0.33-009688.svg)](https://github.com/openresty/headers-more-nginx-module)
## Heroku Buildpack: NGINX-1.17.1
Nginx-buildpack vendors NGINX inside a dyno and connects NGINX to an app server via UNIX domain sockets.

## Requirements
* Your webserver listens to the socket at `/tmp/nginx.socket`.
* You touch `/tmp/app-initialized` when you are ready for traffic.
* You can start your web server with a shell command.

### Language/App Server Agnostic
Nginx-buildpack provides a command named `bin/start-nginx` this command takes another command as an argument. You must pass your app server's startup command to `start-nginx`.

For example, to get NGINX and Unicorn up and running:

```bash
$ cat Procfile
web: bin/start-nginx bundle exec unicorn -c config/unicorn.rb
```

### Setting the Worker Processes
You can configure NGINX's `worker_processes` directive via the
`NGINX_WORKERS` environment variable.

For example, to set your `NGINX_WORKERS` to 8 on a PX dyno:

```bash
$ heroku config:set NGINX_WORKERS=8
```

### Customizable NGINX Config
You can provide your own NGINX config by creating a file named `nginx.conf.erb` in the config directory of your app. Start by copying the buildpack's [default config file](config/nginx.conf.erb).
