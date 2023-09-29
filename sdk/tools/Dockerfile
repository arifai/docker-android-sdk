FROM ubuntu:latest

LABEL io.github.arifai.image.souce https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.source https://github.com/arifai/docker-android-sdk
LABEL org.opencontainers.image.description Android Command Line Tools on Ubuntu Linux
LABEL org.opencontainers.image.licenses MIT

ENV ANDROID_USER android
ENV ANDROID_SDK_TOOLS_VERSION 10406996
ENV ANDROID_HOME /opt/Android/Sdk
ENV ANDROID_PLATFORM_VERSION 34
ENV ANDROID_BUILD_TOOLS_VERSION 34.0.0
ENV ANDROID_BUILD_TOOLS_ROOT ${ANDROID_HOME}/cmdline-tools/latest
ENV JAVA_HOME /usr/lib/jvm/java-19-openjdk-amd64
ENV PATH "$PATH:$ANDROID_BUILD_TOOLS_ROOT/bin:$ANDROID_HOME/platform-tools:$JAVA_HOME/bin"

RUN set -eux; groupadd -r ${ANDROID_USER} \
  && useradd -r -g ${ANDROID_USER} ${ANDROID_USER}

RUN set -eux; mkdir .android && touch .android/repositories.cfg \
  && apt-get update \ 
  && apt-get upgrade -y \
  && apt-get install git wget zip unzip lcov curl xz-utils libglu1-mesa openjdk-19-jdk -y --no-install-recommends \
  && wget -q https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_TOOLS_VERSION}_latest.zip -O sdk-tools.zip \
  && mkdir -p ${ANDROID_HOME}/cmdline-tools \
  && unzip -q sdk-tools.zip -d ${ANDROID_HOME}/cmdline-tools \
  && rm sdk-tools.zip \
  && rm -rf /var/lib/apt/lists/* \
  && mv ${ANDROID_HOME}/cmdline-tools/cmdline-tools ${ANDROID_BUILD_TOOLS_ROOT} 

WORKDIR /${ANDROID_USER}

RUN chown -R ${ANDROID_USER}:${ANDROID_USER} /${ANDROID_USER}

RUN set -eux; yes | sdkmanager --licenses \
  && sdkmanager "build-tools;$ANDROID_BUILD_TOOLS_VERSION" "platform-tools" \
  "platforms;android-$ANDROID_PLATFORM_VERSION"