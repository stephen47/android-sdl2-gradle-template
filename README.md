# android-sdl2-gradle-template

## Synopsis

This is an example project for using libSDL2 (https://www.libsdl.org/) in an Android Gradle project. This project came about as I couldn't find a good example project using libSDL2 in a gradle project. This project will create 2 shared NDK libraries, libSDL2 and libmain, the latter containing a very basic SDL2 program which displays a blue square on a red screen.

## Requirements
- JDK and JRE 8 (I have been using Debian 8 using jessie-backports to get openjdk-8-jre and openjdk-8-jdk)
- Android SDK and NDK (with Android Build-tools 24.0.2 and Android Platform API 23, though these are configurable)
- ANDROID_HOME and ANDROID_NDK_HOME environment variables set (I did this in /etc/environment)

## Before you begin
I have not tested this in Android studio, I have just tested this using the Gradle wrapper command line. It is using gradle-experimental plugin version 0.8.0-beta3 and gradle version 2.14.1.

## Instructions

Download libSDL2 from the website (https://www.libsdl.org/). Copy the src and include directories from the libSDL2 source into SDL2/ so you end up with the following directories:

```
SDL2/src
SDL2/include
```

We also need to copy the example Java file from the libSDL2 source code into our project at the following location (copy from SDL2-2.0.4/android-project/src/org/libsdl/app/SDLActivity.java):

```
app/src/main/java/org/libsdl/app/SDLActivity.java
```

## Compiling the app

```
./gradlew :SDL2:distributeLib
```
This will compile libSDL2 as a shared library.

```
./gradlew :main:distributeLib
```
This will compile our little project (source code in main/src/) as a shared library. You can now skip this step and just run assembleDebug as below. What I would suggest is you compile SDL2 first, commit it to source control, then just build the project as normal (assembleDebug).

```
./gradlew assembleDebug
```
This will build our apk's and output them to app/build/outputs/apk/.

## Thanks

The example libSDL2 program which draws the square on screen was found at https://stackoverflow.com/questions/21890627/drawing-a-rectangle-with-sdl2/21903973#21903973.

This guide was incredibly useful while I tried to figure out how to get this working: http://lazyfoo.net/tutorials/SDL/52_hello_mobile/android_linux/index.php

The Google NDK example projects were very helpful: https://github.com/googlesamples/android-ndk
