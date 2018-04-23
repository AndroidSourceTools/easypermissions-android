<h1 align="center">Runtime Permission Library(Android)</h1>
<p align="center">
  <a href="https://jitpack.io/#mukeshsolanki/App-Runtime-Permissions-Android"><img src="https://jitpack.io/v/mukeshsolanki/App-Runtime-Permissions-Android/month.svg"/></a>
  <a href="https://android-arsenal.com/api?level=9"> <img src="https://img.shields.io/badge/API-14%2B-blue.svg?style=flat" /></a>
  <a href="https://jitpack.io/#mukeshsolanki/App-Runtime-Permissions-Android"> <img src="https://jitpack.io/v/mukeshsolanki/App-Runtime-Permissions-Android.svg" /></a>
  <a href="http://android-arsenal.com/details/3/3790"> <img src="https://img.shields.io/badge/Android%20Arsenal-App--Runtime--Permissions--Android-brightgreen.svg?style=flat" /></a>
  <a href="https://travis-ci.org/mukeshsolanki/App-Runtime-Permissions-Android.svg?branch=master"> <img src="https://travis-ci.org/mukeshsolanki/App-Runtime-Permissions-Android.svg?branch=master" /></a>
  <a href="https://opensource.org/licenses/Apache-2.0"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg"/></a>
  <a href="https://www.paypal.me/mukeshsolanki"> <img src="https://img.shields.io/badge/paypal-donate-yellow.svg" /></a>
  <br /><br />A simple library that will remove all the boilerplate code and speed up your work with new Runtime Permissions introduced in Android M.

## What are Runtime Permissions?

<img src="http://openattitude.com/wp-content/uploads/2015/06/m-permissions-03-location.png" width="500" height="839" />

Google docs is [here](https://developer.android.com/preview/features/runtime-permissions.html). Unlike the traditional way of asking permission Android M increased its security by enforcing apps to ask permissions on the fly as and when the user requests for a feature that requires those permissions. These permissions can also be revoked by the user at any time.
## How to integrate into your app?
Integrating the library into you app is extremely easy. A few changes in the build gradle and your all ready to user Runtime permissions library. Make the following changes to build.gradle inside you app.

Step 1. Add the JitPack repository to your build file. Add it in your root build.gradle at the end of repositories:

```java
allprojects {
  repositories {
    ...
    maven { url "https://jitpack.io" }
  }
}
```
Step 2. Add the dependency
```java
dependencies {
        implementation 'com.github.mukeshsolanki:App-Runtime-Permissions-Android:<latest-version>'
}
```

## How to use the library?
Okay seems like you integrated the library in your project but **how do you use it**? Well its really easy just follow the steps below.

```
 AppPermissions runtimePermission = new AppPermissions(Activity currentActivity);
```
This will create an object of the Runtime Permission class for you. Make sure it's an object of **com.mukesh.permissions.AppPermissions**
To check if the app has a specific permission you can call `runtimePermission.hasPermission(String permission);` or if you want to check 
whether the app has multiple permission you can call `runtimePermission.hasPermission(String[] permissions)`.

<img src="https://d262ilb51hltx0.cloudfront.net/max/800/1*DJTWuO_J8QxKciSAjFWQCg.png" width="400" height="250" />

or like how google requests for multiple permissions

<img src="http://pic.youmobile.org/imgcdn/App-permissions-coming-in-Android-M.jpg" />

You can request for a permission by calling `runtimePermission.requestPermission(String permission, int requestCode)` or request multiple 
permissions by calling `runtimePermission.requestPermission(String[] permissions, int requestCode)`. However you will need to override a 
method on your activity inorder to wait for a callback from the library. Just add this to you activity.

```
@Override public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);
    if (requestCode == mRequestCode) { //The request code you passed along with the request.
    //grantResults holds a list of all the results for the permissions requested.
      for (int grantResult : grantResults) {
        if (grantResult == PackageManager.PERMISSION_DENIED) {
          Log.d("PermissionResult=>", "Denied");
          return;
        }
      }
      Log.d("PermissionResult=>", "All Permissions Granted");
    }
  }
```

That's pretty much it and your all wrapped up.

## Author
Maintained by [Mukesh Solanki](https://www.github.com/mukeshsolanki)

## Contribution
[![GitHub contributors](https://img.shields.io/github/contributors/mukeshsolanki/App-Runtime-Permissions-Android.svg)](https://github.com/mukeshsolanki/App-Runtime-Permissions-Android/graphs/contributors)

* Bug reports and pull requests are welcome.
* Make sure you use [square/java-code-styles](https://github.com/square/java-code-styles) to format your code.

## License
```
Copyright 2018 Mukesh Solanki

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```