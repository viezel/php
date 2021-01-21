# PHP Docker images

The images are minimalistic and ready for production (no node, npm, xdebug etc). Opcache is enabled by default. 

## Images

-	[viezel/php:7.4](https://github.com/viezel/php/blob/master/php/7.4/fpm/Dockerfile)
-	[viezel/php:8.0](https://github.com/viezel/php/blob/master/php/8.0/fpm/Dockerfile)


## How to build

If you want to customize it, then pull down the repo and build it:

```
cd 8.0/fpm
docker build --no-cache -t viezel/php:8.0 -f Dockerfile .
docker push viezel/php:8.0
```



# How to use for Development

Since the image is optimized for production, then we need to change settings to use in development.

You need two extra files: `Dockerfile` and `startup.sh`.

### Dockerfile

``` 
FROM viezel/php:8.0

COPY startup.sh /usr/bin/startup

ENTRYPOINT [ "bash" ]
CMD ["/usr/bin/startup"]
``` 

### startup.sh

``` 
#!/bin/bash

set -e

# disable opcache
sed -i -e "s/opcache.enable=1/opcache.enable=0/" /etc/php/8.0/fpm/php.ini

php-fpm8.0
``` 