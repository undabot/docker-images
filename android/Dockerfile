FROM openjdk:8-jdk
# Environment variables
ENV ANDROID_COMPILE_SDK=30
ENV ANDROID_BUILD_TOOLS=30.0.2
ENV ANDROID_CMDLINE_TOOLS=6858069
ENV PATH=${PATH}:/android-sdk-linux/platform-tools/
ENV ANDROID_HOME=/android-sdk-linux
ENV SDK_URL=https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_CMDLINE_TOOLS}_latest.zip

# Install OS tools
RUN apt-get --quiet update --yes
RUN apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1 build-essential ruby ruby-dev imagemagick

# SDK
RUN echo $SDK_URL
RUN wget --output-document=android-sdk.zip $SDK_URL
RUN mkdir android-sdk-linux
RUN unzip -d android-sdk-linux/cmdline-tools android-sdk.zip
RUN mv android-sdk-linux/cmdline-tools/cmdline-tools android-sdk-linux/cmdline-tools/latest
RUN yes | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager --licenses
RUN echo y | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "platforms;android-${ANDROID_COMPILE_SDK}" >/dev/null
RUN echo y | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "platform-tools" >/dev/null
RUN echo y | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS}" >/dev/null
#RUN echo y | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "extra-android-m2repository" >/dev/null
#RUN echo y | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "extra-google-google_play_services" >/dev/null
#RUN echo y | android-sdk-linux/cmdline-tools/latest/bin/sdkmanager "extra-google-m2repository" >/dev/null
RUN export ANDROID_SDK_ROOT=$PWD/android-sdk-linux
RUN export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools/

RUN wget --quiet --output-document=firebase https://firebase.tools/bin/linux/latest
RUN chmod +x firebase
ENV PATH="firebase:${PATH}"
RUN apt install libcurl4-openssl-dev
RUN gem install bundler
RUN gem install curb -v '0.9.11'