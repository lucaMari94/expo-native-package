# Expo Native Package

This example allows you to create a standalone Expo React Native project by integrating a native package so that you can run Android and IOS code on your devices.


# Project Structure

Project filesystem structure:

 - apps/ - Contains multiple projects, including React Native apps.
 - packages/ - Contains different packages used by your apps.

> mkdir expo-native-package 
> cd expo-native-package 
> mkdir apps  
> mkdir packages

# 1. Initialise a new native package

Once you have set up the basic monorepo structure, create a new module using `create-expo-module` with the flag `no-example` to skip creating the example app.

    npx create-expo-module packages/expo-settings --no-example


## Build the package created

Run one of the apps to ensure everything is working. Then, start the TypeScript compiler inside **packages/expo-settings** to watch for changes and rebuild the module's JavaScript:

    npm run build

## How to use the module in your projects

There are various ways described by the documentation.
For this project we choose to create a tarball of your module and use **npm pack** to install it directly into your project (by running **npm install /path/to/tarball**)

    npm pack
   
 After running this commands, you will notice that a file similar to **expo-settings-0.1.0.tgz** has been created in the package file system.


# 2. Create your first Expo application (StickerSmash)

We will use  [`create-expo-app`](https://docs.expo.dev/more/glossary-of-terms#create-expo-app)  to initialize a new Expo applicarion. It is a command line tool that allows to create a new React Native project with the  `expo`  package installed.

    npx create-expo-app StickerSmash
   
   This command will create a new directory for the project with the name: **StickerSmash**.

## Set up workspace

Now, let's configure `autolinking` so all your apps can use the newly created module. Add the following block to the **package.json** file of each app under the **apps** directory:
```
"expo": {
  "autolinking": {
    "nativeModulesDir": "../../packages"
  }
}
```
## Run prebuild command and compile the app

    npx expo prebuild --clean

This command allows you to generate the native code that allows you to run in the android and IOS environment.
In your project will be created **android** and **ios** folders.

## Add Android SDK directory in local.properties file

A software development kit (SDK) is a set of software tools and programs provided by hardware and software vendors that [developers](https://www.techtarget.com/whatis/definition/software-development) can use to build applications for specific platforms.

In android folder: create file **local.properties** 
```
sdk.dir = /Users/USERNAME/Library/Android/sdk
```

## How to install native package created in your Expo application

To install native module created directly into your project by running **npm install /path/to/tarball**

    npm install /path/to/tarball

## Test the published package

You should now be able to use the module inside your app! To test it, edit the App.js in the app and render the text message from expo-settings.

```
import * as Settings from 'expo-settings';
import { StatusBar } from 'expo-status-bar';
import React from 'react';
import { Text, View } from 'react-native';

export default function App() {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>{Settings.hello()}</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```
## Resources and documentation

[`Expo Documentation`](https://docs.expo.dev)

[`How to use a standalone Expo module in your project`](https://docs.expo.dev/modules/use-standalone-expo-module-in-your-project/#1-initialize-a-new-module)

[`Tutorial: Creating a native module`](https://docs.expo.dev/modules/native-module-tutorial/)
