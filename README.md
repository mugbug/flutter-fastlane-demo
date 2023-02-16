---
marp: true
theme: uncover
class: invert
---

# Flutter* + **Fastlane** = 🚀

<br><br>

###### * or React Native or native iOS/Android ...

---

# Hi, I'm Pedro!

---
###### 📸 Generate screenshots for multiple device sizes
### 🚀 Build and upload a new version to the AppStore
##### 🔐 Handle generate and download certificates and profiles
### 🤖 Configure CI
#### ✈️ Build and upload a beta version to TestFlight

---

# _**fastlane**_  handles tedious tasks so you don’t have to.

---

# Setup Fastlane

```bash
$ cd ios
$ gem install bundler
$ bundle init
$ echo "gem 'fastlane'" >> Gemfile
$ bundle install
# ou simplesmente (não recomendado)
# $ gem install fastlane
```

```bash
alias lane="bundle exec fastlane"
```

---

# $ **lane init**

![height:400px](readme-images/fastlane-init.png)

---

# $ **lane init**
- Automatically create App ID on **Apple Developer Portal**
- Automatically create App on **Apple Store Connect**
- Configured **Appfile**
- Sample **Fastfile**

---

Appfile
```ruby
app_identifier("io.github.mugbug.fastlaneDemo")
apple_id("pedro.zaroni@dextra-sw.com")

itc_team_id("464910") # App Store Connect Team ID
team_id("JZ2QTNWLCN") # Developer Portal Team ID
```

Fastfile
```ruby
desc "Push a new beta build to TestFlight"
lane :beta do
  build_app(workspace: "Runner.xcworkspace", scheme: "Runner")
  upload_to_testflight
end
```

---

# $ **lane beta**
<br>
** ARCHIVE FAILED **

❌  error: "Runner" requires a provisioning profile. Select a provisioning profile in the Signing & Capabilities editor. (in target 'Runner' from project 'Runner')

---
<!-- _class: -->

![bg center 90%](readme-images/code-signing-troubles.png)

---

# Avoid the **frustration** of managing code signing identities

Uncheck _Automatically manage signing_ =]

---

![bg center 80%](readme-images/xcode.png)

---

# Using _**match**_

# Using _**cert**_ and _**sigh**_

---

# Using _**match**_

Private keys + certificates => Github private repo
- Easy to setup new machines with only the repo access
- No need to create a profile for each team member
- Secure 🔒
<br>
⚠️ _match_ requires to revoke existing certificates

---

# Using _**cert**_ and _**sigh**_

- _cert_ will make sure you have a valid certificate and its private key installed on the local machine
- _sigh_ will make sure you have a valid provisioning profile installed locally, that matches the installed certificate

###### Mainly used if you don't want to revoke existing certificates

---

To get started, create a **new private Git repo** and run:

# $ **lane match init**

###### https://codesigning.guide

###### Note: It's also possible to use Google Cloud or Amazon S3 to store the certificates/profiles

---

Matchfile
---

```ruby
# Repo where profiles and certs will be stored
git_url("git@github.com:mugbug/fastlane-demo-certs.git")

storage_mode("git")

# Apple Developer Portal username
username("mugbug@example.com")
```

---

Creating new certificate and profile
```ruby
# Fastfile

desc "Download provisioning profiles"
lane :rematch do
  match(
    type: "appstore", # or development/adhoc
    # git_branch: "my-app",
    username: "mugbug@example.com",
    force: true, # enable to always refresh profiles
    # readonly: true, # enable to prevent refreshes
  )
end
```

---

# $ **lane rematch**

- Generate new certificate and import to local machine
- Create new provisioning profile for Bundle ID
- Setup Passphrase for Match storage
- Encrypt and upload certificate and profile to git repo

---

<!-- _class: -->
![height:500px](readme-images/git-repo.png)

---

# Let's check Xcode's Signing & Capabilities

---

### Why use **match**?

- Full control over what happens
- Share a single code signing identity across the team
- Automatically repair broken and expired credentials
- Clean setup in minutes
- It just works™

---

Sounds good, now let's try this again:

## $ **lane beta**

---

![bg center 90%](readme-images/beta-deploy.png)

---

## Where to go from here?

- Version bump
- Screenshots
- Release notes
- Firebase App Distribution
- Slack message
- Integrate with any CI tool
- ∞ -> beyond! 🚀

<br>

https://docs.fastlane.tools

---

## fastlane.tools just saved you 40 minutes! 🎉

---

References:
---
- [fastlane docs](https://docs.fastlane.tools)
- [Automating Your App's Release Process Using Fastlane](https://www.youtube.com/watch?v=scfOk5SgrKU)
- [A new approach to code signing](https://codesigning.guide)
- [Continuous delivery with Flutter](https://flutter.dev/docs/deployment/cd)
- [Marp gist](https://gist.github.com/yhatt/a7d33a306a87ff634df7bb96aab058b5)
