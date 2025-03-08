## Start a new interactive container image with specific shell name, remove the container after exit interactive shell

```shell
docker run -it --rm openjdk:8-jdk /bin/bash
docker run -it --rm alpine:3.17.2 /bin/ash
```

## Build an image locally with specific tag name

```shell
docker build -t local_image_name .
```

## Publish image to remote repository

```shell
# Create new tag for image
docker tag local_image_name repo/name:tag

# Push to remote
docker push repo/name:tag
```

## Mount path from host OS

```shell
docker run -v path:/path
```

## Set environment variable

```shell
docker run -e POSTGRES_ENV_POSTGRES_USER='bar'
```