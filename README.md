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


Add Firebase, Redux, and device-info to the App.
```
yarn add react-native-firebase react-redux redux-form redux-thunk react-native-device-info
react-native link react-native-firebase react-native-device-info
```

## Platform Specific Setup
[iOS Setup](ios/Readme.md)
[Android Setup](android/Readme.md)