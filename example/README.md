# webrtc_example

Demonstrates how to use the webrtc plugin.

## Getting Started

Make sure your flutter is using the `dev` channel.

```bash
flutter channel dev
./scripts/project_tools.sh create
```

Android/iOS

```bash
flutter run
```

macOS

```bash
flutter run -d macos
```

Web

```bash
flutter run -d web
```

## How to Compile Google's WebRTC Source Code for Android

This works for Linux and Windows with WSL, and might work for Mac but still needs to be confirmed.

#### Useful Links
Google's WebRTC Website: 
https://webrtc.googlesource.com/src/


Tutorial on how to compile the source code: 
https://medium.com/@abdularis/how-to-compile-native-webrtc-from-source-for-android-d0bac8e4c933


If the link above doesn't work, here are the steps:

### Install Prerequisite (Chromium depot_tools)
First we need to download the tools to be able to compile the code (custom git, ninja, gclient, gn)

```bash
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```

Add **depot_tools** into your **PATH** environment variables

```bash
export PATH=$PATH:/path/to/depot_tools
```

### Getting the Source Code
In an empty folder, use the **fetch** command to get the WebRTC Source Code for Android

```bash
fetch --nohooks webrtc_android
```

Then

```bash
gclient sync
```

This takes a **looong** time btw, so have something else you can do in the meantime.

After that's done, go to the **webrtc_android/src/** directory

```bash
cd webrtc_android/src/
```

Now you need to install the dependencies needed to build the source code:
```bash
./build/install-build-deps.sh
```

Make sure you have **OpenJDK** installed and configured properly on your machine!

#### Branches
If you want to see all the available branches, run this command:
```bash
git branch -r
```

To checkout a different branch, you can use this example command:
```bash
git checkout branch-heads/m74
```

To check your current branch, run:
```bash
git branch
```

### Edit the code if you want
Here is when you can edit the source code.  We needed to change the Audio channel in Android so we just replaced **SL_ANDROID_STREAM_VOICE** to **SL_ANDROID_STREAM_MEDIA** and **STREAM_VOICE_CHAT** to **STREAM_MUSIC** in all of the files.

### Compile WebRTC into AAR file
Run this command to compile the source code into a **.arr** file:
```bash
./tools_webrtc/android/build_aar.py
```

This compiles the source code for all supported **cpu types** such as **arm64-v8a, armebai-v7a, x86, x86_64** and then packages these native libraries and .jar libraries into a .aar file.

After it is finished, there should be a **libwebrtc.aar** file in your current directory.

### Linking the Compiled WebRTC AAR file
TODO