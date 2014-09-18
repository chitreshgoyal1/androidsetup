androidsetup
============

android project with phonegap and intellij

Download:

    Download the Java SDK from here: http://www.oracle.com/technetwork/java/javase/downloads/index.html
    Download IntelliJ IDEA Community Edition from here: http://www.jetbrains.com/idea/download/
    Download and unzip the Android SDK or ADT Bundle from here: http://developer.android.com/sdk/index.html
    Download and unzip the PhoneGap package from here: http://phonegap.com/install/   (version 2.9.0 or below)

SDK and NDK path
    
    Right click on Computer -> Properties -> Advanced system settings -> Environment Variables
    Add path for example:
        E:\Installations\adt-bundle-windows-x86_64-20131030\sdk\platform-tools;
        E:\Installations\android-ndk-r9c;
        c:\Program Files\Java\jdk1.6.0_22;


Create a New Project
    
    Select "Application Module" under "Android" & then enter project name and location.
    Click on the New button to create a new SDK mapping.
    On your first run, it will prompt you to configure a Java SDK: Press ok
    Select the location where the Java SDK was installed c:\Program Files\Java\jdk1.6.0_22
    Once you select that, you will be prompted to select the location of the Android SDK i.e. E:\Installations\adt-bundle-windows-x86_64-20131030\sdk\
    After this you will get prompt " Created New Android SDK" : Press ok
    Now Project SDK: is filled with "Android 4.3 plateform(java version "1.6.0_22")
    Click Next and Finish: for target device select emulator if you don't have devices.
    
Setup Cordova

    Unzip cordova2.9.0 
    make folder in Project as: assets/www
    copy cordova.js from unzip cordova2.9.0/lib/android/cordova-2.9.0.js and paste in assets/www/cordova-2.9.0.js
    Right click and select Add As Library
    Right click on main folder and select Open Modules Settings -> add new module and provide zar location
    compile zar file and apply "cordova2.9.0/lib/android/cordova-2.9.0.zar"
    

Crate html file under assets/www folder as: assets/www.index.html
    
    <!DOCTYPE html>
    <html>
    <head>
        <title>Demo Phonegap</title>
        <script type="text/javascript" charset="utf-8" src="cordova.js">
        </script>
    </head>
    <body>
    <h2>Hello Android</h2>
    </body>
    </html>    


MyActivity.java

    package com.example.CordovaExample;
    import android.os.Bundle;
    import org.apache.cordova.DroidGap;
     
    public class MyActivity extends DroidGap {
        /**
         * Called when the activity is first created.
         */
        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            super.loadUrl("file:///android_asset/www/index.html");
        }
    }

AndroidManifest.xml

    <?xml version="1.0" encoding="utf-8"?>
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
              package="com.example.CordovaExample"
              android:versionCode="1"
              android:versionName="1.0">
        <uses-sdk android:minSdkVersion="18"/>
        <supports-screens
                android:largeScreens="true"
                android:normalScreens="true"
                android:smallScreens="true"
                android:resizeable="true"
                android:anyDensity="true"/>
        <uses-permission android:name="android.permission.VIBRATE"/>
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
        <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
        <uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS"/>
        <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.RECEIVE_SMS"/>
        <uses-permission android:name="android.permission.RECORD_AUDIO"/>
        <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS"/>
        <uses-permission android:name="android.permission.READ_CONTACTS"/>
        <uses-permission android:name="android.permission.WRITE_CONTACTS"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.BROADCAST_STICKY"/>
        <application android:label="@string/app_name" android:icon="@drawable/ic_launcher">
            <activity android:name="MyActivity"
                      android:label="@string/app_name"
                      android:screenOrientation="sensor"
                      android:configChanges="orientation|keyboardHidden|screenSize">
                <intent-filter>
                    <action android:name="android.intent.action.MAIN"/>
                    <category android:name="android.intent.category.LAUNCHER"/>
                </intent-filter>
            </activity>
        </application>
    </manifest>


Set Up Virtual Device
    
    Tools -> Android -> AVD Manager
    click on the Device Definitions tab and select Nexus S by Google and then click Create AVD
    Accept the defaults and enter 10 in the SD Card Size
    
    Run & Build
