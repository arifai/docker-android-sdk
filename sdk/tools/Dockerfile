FROM alpine:latest

LABEL io.github.arifai.images.souce https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.source https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.description Android Command Line Tools
LABEL org.opencontainers.image.licenses MIT

ENV ANDROID_SDK_TOOLS_VERSION 10406996
ENV ANDROID_HOME /opt/Android/Sdk
ENV ANDROID_PLATFORM_VERSION 34
ENV ANDROID_BUILD_TOOLS_VERSION 34.0.0
ENV ANDROID_BUILD_TOOLS_ROOT ${ANDROID_HOME}/cmdline-tools/latest
ENV PATH "$ANDROID_BUILD_TOOLS_ROOT/bin:$PATH"
ENV ANDROID_USER android

RUN addgroup -S ${ANDROID_USER} \ 
  && adduser \
  -S ${ANDROID_USER} \
  -G ${ANDROID_USER} -D

RUN mkdir .android && touch .android/repositories.cfg \
  && echo "@testing https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
  && apk update \ 
  && apk add git bash wget zip unzip lcov@testing curl xz mesa openjdk21-jdk@testing --no-cache \
  && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
  && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.35-r1/glibc-2.35-r1.apk \
  && apk add glibc-2.35-r1.apk \
  && wget -q https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS_VERSION}_latest.zip -O sdk-tools.zip \
  && mkdir -p ${ANDROID_HOME}/cmdline-tools \
  && unzip -q sdk-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
  && rm sdk-tools.zip \
  && rm -rf /var/lib/apt/lists/* \
  && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_BUILD_TOOLS_ROOT} \
  && yes | sdkmanager --licenses 

RUN chown -R ${ANDROID_USER}:${ANDROID_USER} .android \
  && chown -R ${ANDROID_USER}:${ANDROID_USER} ${ANDROID_HOME}

USER ${ANDROID_USER}

RUN sdkmanager "build-tools;$ANDROID_BUILD_TOOLS_VERSION" "platform-tools" \
  "platforms;android-$ANDROID_PLATFORM_VERSION"