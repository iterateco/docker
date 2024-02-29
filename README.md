https://docs.docker.com/build/building/multi-platform/

```bash
# To build a multi-arch image, instantiate a custom buildx
docker buildx create --name mybuilder --driver docker-container --bootstrap
docker buildx use mybuilder

# Login is required to push to repo
docker login
# Make sure to switch to mybuilder; builder default may
# change upon docker restart
docker buildx use mybuilder
# Build (for testing)
docker buildx build --platform linux/amd64,linux/arm64 -t <username>/<repository> .
# Build and push to hub docker repo
docker buildx build --platform linux/amd64,linux/arm64 -t <username>/<repository> --push .

# Example:
docker buildx build --platform linux/amd64,linux/arm64 -t iterate/aws-sam-python39 --push .
```

https://circleci.com/docs/2.0/custom-images/#creating-a-custom-image-manually
