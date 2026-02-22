# EcoTaarifa Android Build Guide

This project is a Capacitor wrapper for the EcoTaarifa PWA hosted on InfinityFree.

## Prerequisite: Install Node.js

If you haven't already, install **Node.js LTS** from [nodejs.org](https://nodejs.org/).

## 1. Setup Environment

Navigate to this folder and install dependencies:

```powershell
npm install
```

## 2. PWA Build Mode (Server URL)

This project is configured in `server.url` mode. The APK will load `https://ecotaarifa.wuaze.com/` directly. Updates to your website will be reflected in the app instantly.

## 3. Handling Icons & Splash Screens

Capacitor uses a tool called `@capacitor/assets` to generate all required sizes.

### Recommended Workflow:

1. Place a high-resolution logo (1024x1024 px) in `assets/icon-only.png`.
2. Place a high-resolution splash image (2732x2732 px) in `assets/splash.png`.
3. Run the generator:

```bash
npx @capacitor/assets generate --android
```

Required sizes are handled automatically by this tool.

## 4. Building the APK

You need **Android Studio** installed to build the final APK.

### Step 1: Open in Android Studio

```bash
npx cap open android
```

### Step 2: Build Debug APK (Fast Testing)

1. In Android Studio, go to **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
2. Locate the APK in `android/app/build/outputs/apk/debug/app-debug.apk`.

### Step 3: Build Release Signed APK (Production)

1. Go to **Build > Generate Signed Bundle / APK**.
2. Select **APK** and follow the wizard to create a new keystore and sign the app.

## 5. Troubleshooting Common Errors

### White Screen / Page Not Loading

- **Cause**: The phone has no internet or InfinityFree is blocking the request.
- **Fix**: Ensure `android.allowMixedContent: true` is in `capacitor.config.json` (already added).
- **Fix**: Check that `cleartext: true` is enabled for HTTP testing.

### net::ERR_CLEARTEXT_NOT_PERMITTED

- **Cause**: Android blocks non-HTTPS traffic by default.
- **Fix**: Ensure your `server.url` starts with `https://`.

### Gradle / JDK Issues

- **Cause**: Android Studio needs the correct JDK (usually JDK 17 for modern Gradle).
- **Fix**: Go to **Settings > Build, Execution, Deployment > Build Tools > Gradle** and ensure **Gradle JDK** is set to a valid version.

## 6. Testing Checklist

- [ ] App launches without a white screen.
- [ ] Navigation works (Home, Reports, Profile).
- [ ] Map loads correctly (requires internet).
- [ ] Camera/File upload works (if implemented in PWA).
- [ ] Icons and Splash screen look correct.
