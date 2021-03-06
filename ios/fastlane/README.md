fastlane documentation
================
# Installation

Make sure you have the latest version of the Xcode command line tools installed:

```
xcode-select --install
```

Install _fastlane_ using
```
[sudo] gem install fastlane -NV
```
or alternatively using `brew install fastlane`

# Available Actions
## iOS
### ios deploy_to_testflight
```
fastlane ios deploy_to_testflight
```
Deploy to TestFlight
### ios beta
```
fastlane ios beta
```
Push a new beta build to TestFlight
### ios release
```
fastlane ios release
```
Push a new release build to the App Store
### ios rematch
```
fastlane ios rematch
```
Download provisioning profiles
### ios device
```
fastlane ios device
```
Add new device

----

This README.md is auto-generated and will be re-generated every time [fastlane](https://fastlane.tools) is run.
More information about fastlane can be found on [fastlane.tools](https://fastlane.tools).
The documentation of fastlane can be found on [docs.fastlane.tools](https://docs.fastlane.tools).
