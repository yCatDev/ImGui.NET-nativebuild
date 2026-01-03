# Dear ImGUI Android Build Fork

## Purpose of This Fork
This fork provides a streamlined build process for Dear ImGUI on Android (with future iOS support planned). It uses the specific versions required for ImGUI.NET v1.90.1.1 compatibility.

## Building ImGUI for Android

The method described below has been tested on WSL2 with Ubuntu. First, we need to set up the environment, which is straightforward in our case.

### 1. Clone the Repository
Clone this repository and ensure all submodules are loaded:
```bash
git clone --recursive https://github.com/yCatDev/ImGui.NET-nativebuild.git
```

### 2. Verify Submodule Versions
Navigate to the `cimgui` submodule and verify it's on version **1.90.1dock**. Then check the `imgui` submodule itself and confirm you're on commit **32a3c61**.

### 3. Set Up Android NDK
Download the NDK if you don't have it already:
```bash
cd ~ # Or any other convenient directory
wget https://dl.google.com/android/repository/android-ndk-r27-linux.zip
unzip android-ndk-r*-linux.zip
rm android-ndk-r*-linux.zip
# Important: Specify the path to the extracted folder or existing installation
echo 'export ANDROID_NDK=~/android-ndk-r27' >> ~/.bashrc
echo 'export PATH=$ANDROID_NDK:$PATH' >> ~/.bashrc
source ~/.bashrc
```

Verify the installation by running:
```bash
$ANDROID_NDK_HOME/ndk-build --version
```

### 4. Run the Build Script
```bash
sudo chmod +x build_android.sh
./build_android.sh
```

### What Happens During the Build?
The script automatically downloads and builds the required version of FreeType, then compiles the necessary `.so` library for ImGUI.NET targeting **armeabi-v7a** and **arm64-v8a** architectures in "_out_android" directory. The arm64 version complies with Google Play's 16KB page size requirements. The script builds both debug and release versions for debugging purposes if needed.

## Building ImGUI for iOS
Building for iOS is significantly more complex and may require modifications to ImGUI.NET itself, though it's certainly feasible. Currently, I don't have an immediate need for this, so iOS support is planned for a later date.

## What About Updates?
Updating the Dear ImGUI version requires rebuilding ImGUI.NET and modifying the UImGUI-VR project code (which is what this fork was created for). At this time, I'm not interested in updating and don't plan to do so in the near future. The current version is reasonably up-to-date as of 2026 and should be sufficient for most use cases. However, if you need a newer version, the scripts provided here should work with updated versions—just make sure to properly update all submodules.