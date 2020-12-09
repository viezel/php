# PHP Docker images

The images are minimalistic and ready for production (no node, npm, xdebug etc). 

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