# Flutter Setup

App developement for android, ios, linux, windows, mac

Author

Benedict Thekkel

## Install flutter in WSL

> https://docs.flutter.dev/get-started/install/linux

------------------------------------------------------------------------

``` sh
sudo snap install flutter --classic
```

``` sh
flutter sdk-path
```

## Check FLutter install status

``` sh
flutter doctor
```

## [Install Android Studio in WSL](https://developer.android.com/studio/install)

[Install android studio linux tar gz file](https://developer.android.com/studio?_gl=1*upsjwp*_up*MQ..&gclid=EAIaIQobChMIyOa47dWyhAMV3TV7Bx2isg8PEAAYASAAEgI6LfD_BwE&gclsrc=aw.ds)

![](../Data/android.png)

android.png

### Install using snap

> install java if needed

``` bash
sudo apt install openjdk-18-jdk
```

``` bash

sudo snap install android-studio --classic
```

> check android studio status

``` bash
snap list android-studio
```

> add andriod sdk path to flutter

``` bash
flutter config --android-sdk ~/Android/Sdk/
```

### Manually download and install

go into usr/local and unzip the tar gz file

``` sh
cd /usr/local/
tar xf ~/Downloads/android-studio-version-number-linux.tar.gz
```

### Restart the computer

> Restart the computer

``` bash
wsl --update
wsl --shutdown
```

## Running Android Studio

``` bash
android-studio
```

``` sh
cd /usr/local/
android-studio/bin/studio.sh
```

Open Android Studio -\> More Actions -\> SDK manager -\> SDK Tools -\> Android SDK Command line

![](../Data/sdk_manager.png)

sdk_manager.png

### Configure Android

    Start Android Studio.

    The Welcome to Android Studio dialog displays.

    Follow the Android Studio Setup Wizard.

    Install the following components:
        Android SDK Platform, API 33.0.0
        Android SDK Command-line Tools
        Android SDK Build-Tools
        Android SDK Platform-Tools
        Android Emulator

> To fix android licencing

``` bash
flutter doctor --android-licenses
```

## Install Xming

> Needed to render graphic applications

------------------------------------------------------------------------

``` bash
sudo apt update
sudo apt install x11-apps -y
```

``` bash

xeyes
```

## Install Chrome

``` bash
sudo apt install -y chromium-browser
```

## Connect Phone

### Enable Developer options

> Settings -\> About phone -\> Software Information -\> Build Number

### USB debugging

> Settings -\> Developer Options -\> USB debugging && Wireless debugging

## Connect Phone to Flutter in WSL

### Install adb in windows

> <https://developer.android.com/tools/releases/platform-tools>

add path to windows environment path variable

``` bash
C:\Users\bthek\OneDrive\Documents\platform-tools
```

Check for device connected

    adb devices

Try restarting adb if device doesn’t show up

    adb kill-server
    adb start-server

> Once your device is connected via USB, run the following command to map the desired port to adb.

``` sh
adb tcpip 5555
```

Go to wsl and run

``` bash
adb connnect <ip>:<port>
```

Example:

``` bash
adb connect 192.168.1.4:5555
```

Back to top
