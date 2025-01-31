# Nginx

## How to test nginx input request!
Using the following link:
https://nginx.viraptor.info/

The use case is pretty straight forward. Pass in your nginx configuration and the input url.
At the right section of the image, under the `Final match` section it shows which `location`
the url is entered in.

## How to beautify nginx config
Using the following link:
https://nginxbeautifier.github.io/

## How to reload nginx without downtime from docker-compose
```commandline
docker-compose exec [image-name] nginx -s reload
```

## How to ignore  host not found in upstream "minio:9000" in /etc/nginx/conf.d/nginx.conf
When there is something like below:
```commandline
upstream minio
{
	server container:port;
}
```
And the container is down you get the error
How to tell the nginx to ignore it?

## How to restart nginx in Windows:
```
nginx restart in windows:
@ECHO OFF
cd /nginx
taskkill /f /IM nginx.exe
start nginx
EXIT
```
Thanks to: [Shahryar-Ahmadi](https://github.com/Shahryar-Ahmadi)
