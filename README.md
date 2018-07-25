# Android Gradle Troubleshooting

## What is this?

When building apps using Gradle for android with Android Studio, there are many reasons why a project or module will not build. Some of the errors you get can be quite obscure, and provide no reasonable obvious solution, even when employing very exhaustive research on Google or not Google :P.

For these reasons, it can be very frustrating losing a lot of time, so I have developed this guide to help those with build issues.

## About the steps

Below are tips that will help you get through build issues when an app is compiling for others, but not you. It might also help when it is compiling for no one. I have tried to order the things in priority from top to bottom, but it is impossible to guess exactly why your project(s) are having problems building.

## Why no Windows steps?

I have exclusively been developing for iOS and Android on OSX as it is required to use a Mac to build iOS apps, so I've kind of been forced to use a Mac. Many of these steps may have equivalent steps for Windows.

## Steps

1. Ensure you are using the same branches as other members who can build. This includes the app you are trying to build and it's dependencies.
1. Disable Instant Run
Android Studio -> Preferences -> Build, Execution, Deployment -> Instant Run -> Uncheck the "Enable instant run..." checkbox at the top. The idea was that instant run would improve build times, which it does, however it causes too much inconsitent behaviour to save any time at all.
1. Disable "Offline Work" (you will sometimes get a warning about this one)
Android Studio -> Preferences -> Build, Execution, Deployment -> Global Gradle Settings -> Offline Work (uncheck this). 
	* Disabling Offline work can be a tremendous help towards improving build times, but I reccommend disabling it if things aren't building for now. You can enable offline work once you get things building again.
1. Issue "./gradlew clean" command
1. Close Android Studio, delete your project's .idea and .gradle folders. These are hidden folders, and you will need to show hidden folders to see these if they exist. You may need to reveal hidden files if you're on OSX https://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks/. If your on Windows, you can google this. 
1. Delete your system's gradle cache. Delete the contents of "$HOME/.gradle/caches" as mentioned here https://stackoverflow.com/questions/23025433/how-to-clear-gradle-cache. Note : this seems to be required more often when switching branches with different gradle versions.
1. Invalidate and restart android studio (File -> Invalidate Caches / Restart)
1. Ensure Android Studio is up to date (do NOT use beta channels). While you are free to experiment with the beta channel of Android Studio, here be dragons.
1. Ensure SDKs are up to date
1. Ensure simulators are up to date
1. Uninstall the exiting app
	* Either by the device/simulator's ui
	* Or by issuing "adb uninstall com.yourcompany.app" where the last part is your app package as defined 
1. Ensure youre gradle tools are using the Java Devleopment Kit (JDK), and not the Java Runtime Environment (JRE). When you issue command "./gradlew --version", you should see something like
	```
	Gradle 4.4
	------------------------------------------------------------
	
	Build time:   2017-12-06 09:05:06 UTC
	Revision:     cf7821a6f79f8e2a598df21780e3ff7ce8db2b82
	
	Groovy:       2.4.12
	Ant:          Apache Ant(TM) version 1.9.9 compiled on February 2 2017
	JVM:          1.8.0_101 (Oracle Corporation 25.101-b13)
	OS:           Mac OS X 10.12.6 x86_64
	```
	
	* If not, you may need to specify your java home in your bash profile:
		* export JAVA_HOME=/Applications/Android\ Studio.app/Contents/jre/jdk/Contents/Home/
1. Restart ADB
	* Issue command "adb kill-server"
	* Issue command "adb start-server" (or let android studio start it again for you by hitting run)
1. Reinstall emulator(s) if applicable
1. Reboot the device or simulator either by the UI, or the command "adb reboot"
1. Reboot your system
1. Delete all local local repositories, and pull them down again.
Reinstall Android Studio (if you encountered any update issues when going between versions this is especially true)
1. If using Android Studio 3.0, if you are seeing a build flavour error, add a default build flavour using this guide https://stackoverflow.com/questions/44105127/android-studio-3-0-flavor-dimension-issue
1. Ensure OSX is up to date
1. Ensure Java is up to date


## Who are you?

My name is Jonathan Menard, senior mobile developer for Synacor, working primarily with large telecoms such as AT&T. I have worked on some of the most challenging projects such as Android launchers, video middleware, and Email implementation(s). I have been writing android code since Cupcake / Donut, and iOS code since Objective-C pre ARC era. 

See also:
https://www.linkedin.com/in/jonathan-menard-5a888217/

