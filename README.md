# PHP Docker images

The docker images are divided into two:

* Production 
* Local development

## Production Docker images

These images are minimalistic and ready for production (no node, npm, xdebug etc). Opcache is enabled by default. 

-	[viezel/php:7.4](https://github.com/viezel/php/blob/master/7.4/fpm/Dockerfile)
-	[viezel/php:8.0](https://github.com/viezel/php/blob/master/8.0/fpm/Dockerfile)


## Local development Docker images

These images are created for local development. Xdebug, Node and Yarn are all included. no opcache. 

-	[viezel/php-dev:7.4](https://github.com/viezel/php/blob/master/7.4/dev/Dockerfile)
-	[viezel/php-dev:8.0](https://github.com/viezel/php/blob/master/8.0/dev/Dockerfile)

Can be used together with [Dock a easy docker cli](https://github.com/viezel/dock) tuned for Laravel Development.

## How to build

If you want to customize it, then pull down the repo and build it:

```
cd 8.0/fpm
docker build --no-cache -t viezel/php:8.0 -f Dockerfile .
docker push viezel/php:8.0
```
