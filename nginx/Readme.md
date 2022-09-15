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