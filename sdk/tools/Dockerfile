FROM alpine:latest

LABEL io.github.arifai.images.souce https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.source https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.description Android Command Line Tools on Alpine Linux
LABEL org.opencontainers.image.licenses MIT

ENV ANDROID_SDK_TOOLS_VERSION 10406996
ENV ANDROID_HOME /opt/Android/Sdk
ENV ANDROID_PLATFORM_VERSION 34
ENV ANDROID_BUILD_TOOLS_VERSION 34.0.0
ENV ANDROID_BUILD_TOOLS_ROOT ${ANDROID_HOME}/cmdline-tools/latest
ENV PATH "$PATH:$ANDROID_BUILD_TOOLS_ROOT/bin:$ANDROID_HOME/platform-tools"

RUN mkdir .android && touch .android/repositories.cfg \
  && echo "@testing https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
  && apk update \ 
  && apk add git bash wget zip unzip lcov@testing gcompat curl xz mesa openjdk21-jdk@testing /lib64/ld-linux-x86-64.so.2 --no-cache \
  && wget -q https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS_VERSION}_latest.zip -O sdk-tools.zip \
  && mkdir -p ${ANDROID_HOME}/cmdline-tools \
  && unzip -q sdk-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
  && rm sdk-tools.zip \
  && rm -rf /var/lib/apt/lists/* /var/cache/apk/* /usr/share/man/* /usr/share/doc \
  && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_BUILD_TOOLS_ROOT} \
  && yes | sdkmanager --licenses 

RUN sdkmanager "build-tools;$ANDROID_BUILD_TOOLS_VERSION" "platform-tools" \
  "platforms;android-$ANDROID_PLATFORM_VERSION"