# Base container
FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Install required packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget unzip curl git libglu1-mesa \
    && rm -rf /var/lib/apt/lists/*

# Install Android SDK Command-line tools
ENV ANDROID_SDK_ROOT=/opt/android-sdk
ENV PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools

RUN mkdir -p $ANDROID_SDK_ROOT/cmdline-tools && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O tools.zip && \
    unzip tools.zip && \
    mv cmdline-tools $ANDROID_SDK_ROOT/cmdline-tools/latest && \
    rm tools.zip

# Accept licenses + install SDK components
RUN yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"

# Gradle JVM optimization
ENV GRADLE_OPTS="-Xmx6g -Dkotlin.daemon.jvm.options=-Xmx2g"
