# Docker Image Android Tools & Android NDK

You can run it using CI or locally via Docker.

# Usage
## Dockerfile

Use as base image in `Dockerfile`

```Dockerfile
FROM ghcr.io/arifai/android-sdk:ndk-latest
```
## GitLab CI

Use as base image in `.gitlab-ci.yml`

```yml
image: ghcr.io/arifai/android-sdk:ndk-latest

stages:
  - build

build:
  stage: build
  ...
```