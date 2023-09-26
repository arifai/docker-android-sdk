[![Publish Registry to ghcr.io](https://github.com/arifai/docker-android-sdk/actions/workflows/publish.yaml/badge.svg?branch=main)](https://github.com/arifai/docker-android-sdk/actions/workflows/publish.yaml)

# Docker Image Android Tools & Android NDK

You can run it using CI or locally via Docker.

# Usage
## Dockerfile

Use as base image in `Dockerfile`

```Dockerfile
FROM ghcr.io/arifai/android-sdk:latest
```
## GitLab CI

Use as base image in `.gitlab-ci.yml`

```yml
image: ghcr.io/arifai/android-sdk:latest

stages:
  - build

build:
  stage: build
  ...
```