# Android Setup

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
## Add AppCenter Versioning off of APPCENTER_BUILD_ID
Add the following to `android/app/build.gradle`
```
/** 
 * BUILD VERSIONING
 */
def lastAppcenterReleaseBuildId = 1
def appcenterBuildId = (System.getenv("APPCENTER_BUILD_ID") ?: 1).toInteger()
def buildId = (appcenterBuildId % lastAppcenterReleaseBuildId) ?: appcenterBuildId
logger.warn("AppCenterBuildId: ${appcenterBuildId}\nBuildId: ${buildId}")
android {
    defaultConfig {
        ...
        versionCode appcenterBuildId
        versionName "0.1.${buildId}"
        ...
    }
```

## Add Build Flavors for different builds
Add the following to `android/app/build.gradle`
```
android {
   ...
   // Added for environment builds 
   productFlavors {
        dev {
            dimension "environment"
            applicationIdSuffix '.dev'
        }
        prod {
            dimension "environment"
        }
    }
    ...
}
```

### Change App Name for dev
```bash
mkdir -p android/app/src/dev/res/values
echo '<resources>
    <string name="app_name">FireApp Dev</string>
</resources>
' > android/app/src/beta/res/values/strings.xml
```