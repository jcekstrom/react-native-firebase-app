# react-native-firebase-app

## react-native setup
First we need to install react-native-cli:
```
yarn global add react-native-cli
```

Next initialize your application.
```
react-native init <tmp_appname>
```


Rename the app and setup better bundle identifiers.
```
yarn add --dev react-native-rename
react-native-rename -b <bundle identifier> <app_name>
```

```
mkdir src
mv App.js src
```

Add jvm args to `android/gradle.properties` avoid issues with running out of memory
```
org.gradle.jvmargs=-Xmx2048M
```

Upgrade gradle in `android/app/build.gradle`.
```
buildscript {
    repositories {
        google()
        jcenter()
        maven {
            url 'https://maven.fabric.io/public'
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.4'
        classpath 'com.google.gms:google-services:4.0.1'
        classpath 'io.fabric.tools:gradle:1.25.4'
        // NOTE: Do not place your application dependencies here; they belong 
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        mavenLocal()
        google()
        jcenter()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
        maven {
            url 'https://maven.google.com/'
            name 'Google'
        }
    }
}

ext {
    buildToolsVersion = "26.0.3"
    minSdkVersion = 16
    compileSdkVersion = 26
    targetSdkVersion = 26
    supportLibVersion = "26.1.0"
}
```

Add Firebase, Redux, and device-info to the App.
```
yarn add react-native-firebase react-redux redux-form redux-thunk react-native-device-info
react-native link react-native-firebase react-native-device-info
```