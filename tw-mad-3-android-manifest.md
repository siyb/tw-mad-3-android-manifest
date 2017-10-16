% MAD - Android 3: The Android Manifest
% Patrick Sturm
% 16.10.2017

## Information

* Any issues with this presentation? Write a ticket or send me a pull request ;).
* Repo: [https://github.com/siyb/tw-mad-3-android-manifest](https://github.com/siyb/tw-mad-3-android-manifest)

# Agenda

## Agenda

* General AndroidManifest information
* Declaring Permissions

# AndroidManifest

## AndroidManifest - 1 - Resources

* Lesson:
    * [http://developer.android.com/guide/topics/manifest/manifest-intro.html](http://developer.android.com/guide/topics/manifest/manifest-intro.html)
* Lesson:
    * [http://developer.android.com/guide/topics/security/permissions.html](http://developer.android.com/guide/topics/security/permissions.html)
    
## AndroidManifest - 2 - Basics

* We have heard about the AndroidManifest before
* It is essential, since it is used to compile Android components into an application
* It also serves other purposes
    * Version restrictions
    * Screen sizes
    * Permissions (bidirectional: requires / offers)
    * Package Name (UNIQUE application identifier!)
    * Etc.
* The AndroidManifest will be used by the Google Play and the Android system (e.g. determine if an app is installable)

## AndroidManifest - 2 - Basics cont.

* We have seen how the AndroidManifest is used to register an Activity

```xml
<activity android:name=".MyFirstActivity" 
  android:icon="@drawable/app_icon"> 
  <intent-filter> 
    <action 
      android:name="android.intent.action.MAIN" /> 
    <category 
      android:name="android.intent.category.LAUNCHER"/> 
  </intent-filter> 
</activity>
```
* In this example, we also register so called intent-filters For now, it’s enough to mention that MyFirstActivity reacts to implicit as well as explicit Intents
* .MyFirstActivity – the . is used as a replacement for the app’s package name

## AndroidManifest - 3 - Complete Manifest

```xml
<manifest xmlns:android=
    "http://schemas.android.com/apk/res/android" 
  package="com.example.test" 
  android:versionCode="1" 
  android:versionName="1.0"> 
  <uses-sdk 
    android:minSdkVersion="8" 
    android:targetSdkVersion="15" />
  <uses-permission android:name=
    "android.permission.INTERNET"/> 
   ...
</manifest>
```

## AndroidManifest - 4 - Complete Manifest cont.

```xml
<manifest>
    ...
    <application 
      android:icon="@drawable/ic_launcher" 
      android:label="@string/app_name" 
      android:theme="@style/AppTheme" > 
      <activity 
        android:name=".MainActivity" 
        android:label="@string/title_activity_main" > 
        <intent-filter> 
          <action android:name=
            "android.intent.action.MAIN" /> 
          <category android:name=
            "android.intent.category.LAUNCHER" /> 
        </intent-filter> 
      </activity> 
    </application> 
</manifest>
```

## AndroidManifest - 5 - Complete Manifest Explained

* Lets go through the AndroidManifest step by step (the AndroidManifest used here is the one that Android Studio will autogenerate for you)
* The manifest element
    * package – your application’s package, must be unique (otherwise you will get conflicts when attempting to upload your app to Google Play or a test device).
    * Convention: domain backwards, append application name: com.foobar.myapplication
    * android:versionName: Can be anything really, version string displayed to the user
    * android:versionCode: An integer value representing the version of your application. You _should_ increment this value every time you release a new version.

## AndroidManifest - 6 - Complete Manifest Explained cont.

* The uses-sdk element
    * android:minSdkVersion: Mininum version required to run your application.
    * android:targetSdkVersion: The version your application is targeted at. Suggestion: use the same level as you use as build target.
    * android:maxSdkVersion: Used to restrict the maximum version your app will run on. Please try to avoid this setting!
    * You might ask yourself: if I specify android:minSdkVersion=“10” and android:targetSdkVersion=“16” and use SDK version 16 as a build target, how do I know if a certain functionality from SDK version 16 is available on SDK version 10? -> Android lint (http://tools.android.com/tips/lint) - NewApi Error
* The uses-permission element
    * Each permission your app requires needs to be provided in an uses-permission element
        
## AndroidManifest - 7 - Complete Manifest Explained

* The application element
    * Pretty important, that’s where we define our components
    * The overall application Theme is defined here as well …
    * … so is the application’s icon
    
# Declaring Permissions

## Declaring Permissions - 1 - Attributes

* Can be done using the <permission> element
    * android:label: Permission’s name, will be displayed to user
    * android:description: Descriptive text, will be displayed to user
    * android:permissionGroup: May be used to group multiple permissions
    * android:protectionLevel: Tells the system how the user is informed about the permission and who can utilize the permission
    
## Declaring Permissions - 1 - Protection Level

* android:protectionLevel can have the following values:
    * normal: Low risk, user will not explicitly asked for approval, isolated application level feature access
    * dangerous: Higher risk, i.e. access to private user data, user has to approve explicitly
    * signature: Automatically grants the permission to applications signed with the same certificate, does not require user approval
    * signatureOrSystem: Automatically grants the permission to system applications and applications that have been signed with the same certificate
    * system: Flag for system applications
    * Development: Flag for development applications
    
## Declaring Permissions - 3 - URI Permissions - ContentProvider

* Since ContentProvider may offer a variety of ways to access and manipula te data, it may not be sufficient to use a single permission
* This is where URI permissions come into play, add this attribute to your ContentProvider definition
    * android:grantUriPermissions (boolean)
* If you fire an Intent, you may set the Intent. FLAG_GRANT_READ_URI_PERMISSION or Intent.FLAG_GRANT_WRITE_URI_PERMISSION
* Setting these flags will grant read/write access to the URI contained in the Intent’s data and ClipData

# Any Questions?


