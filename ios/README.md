# iOS Setup
There is a significant amount of iOS Platform specific setup that must take place.

## Create Podfile
You can look at ios/Podfile as an example.

## Scheme Management
Yee Wong has created a nice tutorial [Building multiple versions of a React Native app](https://medium.com/@ywongcode/building-multiple-versions-of-a-react-native-app-4361252ddde5).
Schemes allow us to create specific build targets for different environments, like Dev and Prod.

### Create New Build Configurations
* Open iOS Workspace in XCode
* Select the project
* Select the Info Tab
* Add new Configurations duplicating Debug and Release, and call them something like Dev.Debug and Dev.Release

### Duplicate Scheme
* Click on current scheme
* Scroll to the bottom and click "Edit Scheme..."
* Click "Duplicate Scheme" and name is something like "Dev"
* Change "Run" to "Dev.Debug"
* Change "Archive to "Dev.Release"

### Add react-native-schemes-manager to fix up issues with node modules, etc.
```bash
yarn add --dev react-native-schemes-manager
```

### Change Dev App Name
* Open FireApp Target
* Open Build Settings Tab
* Search for "product name"
* Click on "Product name" to expand
* Edit name for "Dev" variants

### Run Dev/Prod side by side
* Select FireApp Target
* * Select Info Tab
* * * Add change the "Bundle identifier" to `$(PRODUCT_BUNDLE_IDENTIFIER)$(BUNDLE_ID_SUFFIX)`
* * Select Build Settings Tab
* * * Click the + to add a user defined setting
* * * Add `BUNDLE_ID_SUFFIX`
* * * Expand `BUNDLE_ID_SUFFIX`
* * * Set `.dev` on the "Dev" variants
  