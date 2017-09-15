# Create a calorie counter mobile app using Watson Visual Recognition

In this developer journey, we will create a calorie counter mobile app using Apache Cordova, Node.js and Watson Visual Recognition. This mobile app extracts nutritional information from captured images of food items.

Currently this mobile app only runs on Android, but can be easily ported to iOS.

![](doc/source/images/architecture.png)

## Flow

1. User interacts with the mobile app and captures an image.
2. The image is passed to the server application which uses Watson Visual Recognition Service to analyze the images and Nutritionix API to provide nutritional information.
3. Data is returned to the mobile app for display.

## With Watson

Want to take your Watson app to the next level? Looking to leverage Watson Brand assets? Join the [With Watson](https://www.ibm.com/watson/with-watson/) program which provides exclusive brand, marketing, and tech resources to amplify and accelerate your Watson embedded commercial solution.

## Included components

* [Watson Visual Recognition](https://www.ibm.com/watson/developercloud/visual-recognition.html): Visual Recognition understands the contents of images - visual concepts tag the image, find human faces, approximate age and gender, and find similar images in a collection.

## Featured Technologies

* Mobile: Systems of engagement are increasingly using mobile technology as the platform for delivery.
* [Nutritionix API](https://developer.nutritionix.com/): The largest verified database of nutrition information.
* [Node.js](https://nodejs.org/): An asynchronous event driven JavaScript runtime, designed to build scalable applications.

# Watch the Video

TODO

# Steps

This journey contains several pieces. The app server communicates with the Watson Visual Recognition service. The mobile application is built locally and run on the Android phone.

## Deploy the Server Application to Bluemix

[![Deploy to Bluemix](https://deployment-tracker.mybluemix.net/stats/3999122db8b59f04eecad8d229814d83/button.svg)](https://bluemix.net/deploy?repository=https://github.com/IBM/watson-calorie-counter.git)

1. Press the above ``Deploy to Bluemix`` button and then click on ``Deploy``.

2. In Toolchains, click on Delivery Pipeline to watch while the app is deployed.

![](doc/source/images/toolchain-pipeline.png)

3. To see the app and services created and configured for this journey, use the Bluemix dashboard. The app is named `watson-calorie-counter` with a unique suffix. The following services are created and easily identified by the `wcc-` prefix:
    * wcc-visual-recognition

> Note: Make note of the `watson-calorie-counter` URL route - it will be required for later use in the mobile app.

To complete the installation, perform the following steps:

1. [Clone the repo](#1-clone-the-repo)
2. [Obtain a Nutritionix API ID and key](#2-obtain-a-nutritionix-api-id-and-key)
3. [Update config values for the Mobile App](#3-update-config-values-for-the-mobile-app)
4. [Install Android Mobile Development Framework](#4-install-android-mobile-development-framework)
5. [Add Android platform and plug-ins](#5-add-android-platform-and-plug-ins)
6. [Setup your Android phone](#6-setup-your-android-phone)
7. [Build and run the mobile app](#7-build-and-run-the-mobile-app)

## 1. Clone the repo

Clone the `watson-calorie-counter`repo locally. In a terminal, run:

```
$ git clone https://github.com/IBM/watson-calorie-counter.git
```

## 2. Obtain a Nutritionix API ID and key

Nutritionix data is used to gather nutritional information of an analyzed image. Instructions for obtaining a key can be found at [Nutritionix.com](https://developer.nutritionix.com/).

> Note: Make note of the API ID and key - they will be required for later use in the mobile app.

## 3. Update config values for the Mobile App

Edit `mobile/www/config.json` and update the setting with the values retrieved previously.

```
"BLUEMIX_SERVER_URL": "<add-bluemix-server-url>",
"NUTRITIONIX_APP_ID": "<add-nutritionix-app-id>",
"NUTRITIONIX_APP_KEY": "<add-nutritionix-app-key>"
```

## 4. Install Android Mobile Development Framework

For this journey, we will be using the Cordova Android framework.

Installation instruction can be found on the [Cordova Android Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html).

This installation will require installing the [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) as well as [Android Studio](https://developer.android.com/studio/index.html).

From `Android Studio`, download and install the desired API Level for the SDK. To do this:

* Launch `Android Studio` and accept all defaults.
* Click on the SDK Manager Icon in the toolbar.
* Navigate to `Appearance & Behavior` -> `System Settings` -> `Android SDK`
* Select desired API Levels (select all >= 23).
* Click apply to download and install.

Once you have completed all of the required installs and setup, you should have the following environment variables set:

```
JAVA_HOME
ANDROID_HOME
ANDROID_SDK_HOME
PATH
```

> Note: For additonal help setting these environment variables, refer to the  [Troubleshooting](#troubleshooting) section below.

### 5. Add Android platform and plug-ins

Add the Android platform as the target for your mobile app. Then install plug-ins to provide access to device-level features.

```
$ cd mobile
$ cordova platform add android

# ensure that everything has been installed correctly
$ cordova requirements

$ cordova plugin add cordova-plugin-camera
$ cordova plugin add cordova-plugin-file-transfer
```

### 6. Setup your Android phone

In order to run the mobile app on your phone, you will need to enable `developer options` and `web debugging`.

> Note: Please refer to documentation on your specific phone to set these options.

Attach your Android phone to your computer.

Install [Android File Transfer](https://www.android.com/filetransfer/) on your computer to enable file transfer between your computer and phone.

### 7. Build and run the mobile app

```
$ cd mobile
$ cordova build android
$ cordova run android
```

At this point, the app named `Calorie Counter` should come up on your phone. Press the `Capture Image` button to transfer to your phone camera. Take a photo of a food item and press `OK`. Analysis data will then be displayed.

# Sample Output

<img src="doc/source/images/output1.jpg" width="250">  <img src="doc/source/images/output2.jpg" width="250">

# Links

* [Watson Node.js SDK](https://github.com/watson-developer-cloud/node-sdk)

# Troubleshooting

* `cordova run android` error: Failure [INSTALL_FAILED_UPDATE_INCOMPATIBLE]

> The `Calorie Counter` app is already installed on your phone and incompatible with the version you are now trying to run. Uninstall the current version and try again.

* `cordova run android` error: No target specified and no devices found, deploying to emulator

> Ensure that your phone is plugged into your computer and you can access it from the Android File Transfer utility (see Step #6 above).

* How to determine proper values for environment variables:

Open `Android Studio` and navigate to `File` -> `Project Structure` -> `SDK
Location`. This location value will serve as the base for your environement variables. For example, if the location is `/users/joe/Android/sdk`, then:

```
export ANDROID_HOME=/users/joe/Android/sdk
export ANDROID_SDK_HOME=/users/joe/Android/sdk/platforms/android-<api-level>
export PATH=${PATH}:/users/joe/Android/sdk/platform-tools:/users/joe/Android/sdk/tools
```

# License

[Apache 2.0](LICENSE)

# Privacy Notice

If using the Deploy to Bluemix button some metrics are tracked, the following
information is sent to a [Deployment Tracker](https://github.com/IBM-Bluemix/cf-deployment-tracker-service) service
on each deployment:

* Node.js package version
* Node.js repository URL
* Application Name (`application_name`)
* Application GUID (`application_id`)
* Application instance index number (`instance_index`)
* Space ID (`space_id`)
* Application Version (`application_version`)
* Application URIs (`application_uris`)
* Labels of bound services
* Number of instances for each bound service and associated plan information

This data is collected from the `package.json` file in the sample application and the ``VCAP_APPLICATION``
and ``VCAP_SERVICES`` environment variables in IBM Bluemix and other Cloud Foundry platforms. This
data is used by IBM to track metrics around deployments of sample applications to IBM Bluemix to
measure the usefulness of our examples, so that we can continuously improve the content we offer
to you. Only deployments of sample applications that include code to ping the Deployment Tracker
service will be tracked.

## Disabling Deployment Tracking

To disable tracking, simply remove ``cf_deployment_tracker.track()`` from the
``app.js`` file in the top level directory.
