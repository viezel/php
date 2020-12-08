# PHP Docker images

- Minimalistic
- Ready for production

## How to build

Example of building one of the images

```
cd 8.0/fpm
docker build --no-cache -t viezel/php:8.0-fpm -f Dockerfile .
docker push viezel/php:8.0-fpm
```