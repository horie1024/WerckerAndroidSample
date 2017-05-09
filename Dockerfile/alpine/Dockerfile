FROM alpine:3.5

MAINTAINER Ryosuke Horie

# Install sudo, openjdk8, openssl
RUN apk update \
  && apk upgrade \
  && apk add openjdk8 \
  && apk add bash \
  && apk add --update openssl \
  && apk add sudo \
  && sudo apk add libstdc++ \
  && apk del sudo \
  && rm -rf /var/cache/apk/*

# Download Android SDK
RUN cd /usr/local \
  && mkdir -p android-sdk/licenses \
  && cd android-sdk \
  && wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip \
  && unzip sdk-tools-linux-3859397.zip \
  && rm -rf /usr/local/android-sdk/sdk-tools-linux-3859397.zip

# Environment variables
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV ANDROID_HOME /usr/local/android-sdk
ENV PATH $ANDROID_HOME/tools/bin:$ANDROID_HOME/tools:$PATH

# Update of Android SDK
RUN bash \
  && echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > "$ANDROID_HOME/licenses/android-sdk-license" \
  && echo -e "\n84831b9409646a918e30573bab4c9c91346d8abd" > "$ANDROID_HOME/licenses/android-sdk-preview-license" \
  && sdkmanager "platforms;android-25" "build-tools;25.0.3" \
                "extras;android;m2repository" "extras;google;m2repository"
