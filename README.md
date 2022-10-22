# Get Started


## Docker
Image: https://hub.docker.com/r/klakegg/hugo/

### Build and serve
```
docker run --rm -it -v ${PWD}:/src -p 1313:1313 klakegg/hugo:ext-alpine server
```
