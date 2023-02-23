https://docs.docker.com/build/building/multi-platform/

```bash
# To build a multi-arch image, instantiate a custom buildx
docker buildx create --name mybuilder --driver docker-container --bootstrap
docker buildx use mybuilder

# Build and push to hub docker repo
docker buildx build --platform linux/amd64,linux/arm64 -t <username>/<repository> --push .
```

https://circleci.com/docs/2.0/custom-images/#creating-a-custom-image-manually
