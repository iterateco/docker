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
# Example: Build only and output to build.log:
# https://forums.docker.com/t/capture-ouput-of-docker-build-into-a-log-file/123178/2
docker buildx build --platform linux/amd64,linux/arm64 -t iterate/aws-sam-python39 . 2>&1 | tee build.log

# Build and force rebuild from scratch without using cache
docker buildx build --platform linux/amd64,linux/arm64 --no-cache -t <username>/<repository> .

# Build and push to hub docker repo
docker buildx build --platform linux/amd64,linux/arm64 -t <username>/<repository> --push .
# Example 1: build and push to docker hub
docker buildx build --platform linux/amd64,linux/arm64 -t iterate/aws-sam-python39 --push .
```

https://circleci.com/docs/2.0/custom-images/#creating-a-custom-image-manually
