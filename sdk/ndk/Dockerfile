FROM ghcr.io/arifai/android-sdk:latest

LABEL org.opencontainers.image.source https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.description Android NDK on Ubuntu Linux
LABEL org.opencontainers.image.licenses MIT

ENV ANDROID_NDK_VERSION 26.2.11394342

RUN set -eux; yes | sdkmanager "ndk;$ANDROID_NDK_VERSION"
