# **🚀 Automating React Native Android App Release to Google Play Store using Docker & GitHub Actions**  

To **build & release** a **React Native** app for **Android** on the **Google Play Store**, we will use:  
✅ **Docker** for consistent builds  
✅ **GitHub Actions** for CI/CD  
✅ **Fastlane** for automated Play Store uploads  

---

## **🔹 Step 1: Set Up Docker for Android Build**
Create a `Dockerfile` for building the React Native Android app:

### **📌 `Dockerfile`**
```dockerfile
# Use Node.js and Java SDK base image
FROM reactnativecommunity/react-native-android:latest

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json yarn.lock ./
RUN yarn install

# Copy the entire project
COPY . .

# Grant execute permissions
RUN chmod +x android/gradlew

# Build the release APK/AAB
RUN cd android && ./gradlew bundleRelease

# Output directory (APK/AAB will be stored here)
CMD ["cp", "-r", "android/app/build/outputs", "/app"]
```

---

## **🔹 Step 2: Configure Fastlane for Play Store Upload**
Fastlane automates the Play Store upload process.

### **📌 Install Fastlane**
In your project root, install Fastlane:
```sh
cd android && bundle init
bundle add fastlane
bundle install
```
Then, initialize Fastlane:
```sh
fastlane init
```

### **📌 `android/fastlane/Fastfile`**
Edit `android/fastlane/Fastfile`:
```ruby
default_platform(:android)

platform :android do
  desc "Build AAB and Upload to Google Play"
  lane :deploy do
    gradle(task: "bundle", build_type: "Release")
    upload_to_play_store(track: "internal")
  end
end
```

---

## **🔹 Step 3: Create a Keystore for Signing**
Google Play requires a signed build. Generate a keystore:

```sh
keytool -genkeypair -v -keystore android/app/release.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

Update `android/gradle.properties`:
```
MYAPP_RELEASE_STORE_FILE=release.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=your-store-password
MYAPP_RELEASE_KEY_PASSWORD=your-key-password
```

**Securely store these credentials in GitHub Secrets.**

---

## **🔹 Step 4: Set Up GitHub Actions CI/CD**
### **📌 `.github/workflows/release.yml`**
```yaml
name: Build & Release React Native Android App

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Docker
        run: docker build -t rn-build .

      - name: Run Build
        run: docker run --rm -v ${{ github.workspace }}:/app rn-build

      - name: Upload Artifact
        uses: actions/upload-artifact@v3
        with:
          name: android-build
          path: android/app/build/outputs

  release:
    needs: build
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Download Build Artifacts
        uses: actions/download-artifact@v3
        with:
          name: android-build
          path: android/app/build/outputs

      - name: Set up Ruby & Fastlane
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: 3.0

      - name: Install Fastlane
        run: cd android && bundle install

      - name: Upload to Google Play
        run: cd android && bundle exec fastlane deploy
        env:
          GOOGLE_PLAY_JSON_KEY: ${{ secrets.GOOGLE_PLAY_JSON_KEY }}
          MYAPP_RELEASE_STORE_PASSWORD: ${{ secrets.MYAPP_RELEASE_STORE_PASSWORD }}
          MYAPP_RELEASE_KEY_PASSWORD: ${{ secrets.MYAPP_RELEASE_KEY_PASSWORD }}
```

---

## **🔹 Step 5: Securely Store Play Store Credentials**
1. **Generate Google Play API JSON Key**:
   - Go to **Google Play Console** → **API Access** → **Create Service Account**.
   - Grant **"Release Manager"** role.
   - Download the JSON key file.

2. **Add GitHub Secrets** (`Settings` → `Secrets` → `Actions`):
   - `GOOGLE_PLAY_JSON_KEY`: Paste the content of the JSON key.
   - `MYAPP_RELEASE_STORE_PASSWORD`: Your keystore password.
   - `MYAPP_RELEASE_KEY_PASSWORD`: Your key alias password.

---

## **🎯 Done!**
Now, every push to `main` will:  
✅ **Build** your React Native app inside Docker  
✅ **Generate** an AAB (Android App Bundle)  
✅ **Sign** it with your keystore  
✅ **Upload** it to **Google Play (internal track)** automatically 🚀  

Would you like to add **iOS support** as well? 😊
