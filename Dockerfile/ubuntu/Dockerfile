FROM ubuntu:16.04

MAINTAINER Ryosuke Horie

# Install sudo
RUN apt-get update \
  && apt-get -y install sudo \
  && useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

# Install 32bit lib
RUN sudo apt-get -y install lib32stdc++6 lib32z1

# Install Java8
RUN apt-get install -y software-properties-common curl \
    && add-apt-repository -y ppa:openjdk-r/ppa \
    && apt-get update \
    && apt-get install -y openjdk-8-jdk

# Download Android SDK
RUN sudo apt-get -y install wget unzip \
  && cd /usr/local \
  && mkdir -p android-sdk/licenses \
  && cd android-sdk \
  && wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip \
  && unzip sdk-tools-linux-3859397.zip \
  && rm -rf /usr/local/android-sdk/sdk-tools-linux-3859397.zip

# Environment variables
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV ANDROID_HOME /usr/local/android-sdk
ENV PATH $ANDROID_HOME/tools/bin:$ANDROID_HOME/tools:$PATH

# Update of Android SDK
RUN echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > "$ANDROID_HOME/licenses/android-sdk-license" \
  && echo -e "\n84831b9409646a918e30573bab4c9c91346d8abd" > "$ANDROID_HOME/licenses/android-sdk-preview-license" \
  && sdkmanager "platforms;android-25" "build-tools;25.0.3" \
                "extras;android;m2repository" "extras;google;m2repository"