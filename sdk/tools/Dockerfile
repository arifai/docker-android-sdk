FROM alpine:latest

LABEL io.github.arifai.image.souce=https://github.com/arifai/docker-android-sdk

ENV ANDROID_SDK_TOOLS_VERSION 10406996
ENV ANDROID_HOME /opt/Android/Sdk
ENV ANDROID_PLATFORM_VERSION 34
ENV ANDROID_BUILD_TOOLS_VERSION 34.0.0
ENV ANDROID_BUILD_TOOLS_ROOT ${ANDROID_HOME}/cmdline-tools/latest
ENV PATH "$ANDROID_BUILD_TOOLS_ROOT/bin:$PATH"

RUN mkdir .android && touch .android/repositories.cfg \
  && echo "@testing https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
  && apk add --update --no-cache git bash wget zip unzip lcov@testing curl xz xz-dev mesa mesa-dev openjdk21@testing \
  && wget -q https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS_VERSION}_latest.zip -O sdk-tools.zip \
  && mkdir -p ${ANDROID_HOME}/cmdline-tools \
  && unzip -q sdk-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
  && rm sdk-tools.zip \
  && rm -rf /var/lib/apt/lists/* \
  && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_BUILD_TOOLS_ROOT} \
  && yes | sdkmanager --licenses 

RUN sdkmanager "build-tools;$ANDROID_BUILD_TOOLS_VERSION" "platform-tools" \
  "platforms;android-$ANDROID_PLATFORM_VERSION"