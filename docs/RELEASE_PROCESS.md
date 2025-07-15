# Release Process Guide

## 🎯 **Yes! APK and iOS builds WILL be released on GitHub releases with correct tags!**

Here's exactly how the release process works:

## 📱 **Release Assets**

### **Android APK**
- ✅ **Attached to GitHub Release**: The APK will be directly attached to the GitHub release
- ✅ **Proper Tagging**: Named as `app-release-{version}.apk` (e.g., `app-release-1.0.0.apk`)
- ✅ **Downloadable**: Users can download the APK directly from the GitHub release page
- ✅ **Version Tagged**: Each release is tagged with the version from `package.json`

### **iOS Build**
- ✅ **Attached to GitHub Release**: The iOS build will be attached as a zip file
- ✅ **Proper Tagging**: Named as `ios-build-{version}.zip` (e.g., `ios-build-1.0.0.zip`)
- ✅ **For Distribution**: Can be used for TestFlight or App Store distribution
- ✅ **Version Tagged**: Properly versioned with the app version

### **Web Deployment**
- ✅ **Deployed to Vercel**: Automatic deployment to your Vercel domain
- ✅ **Live URL**: Accessible immediately after deployment
- ✅ **Version Tagged**: Each deployment corresponds to the GitHub release

## 🔄 **Release Workflow**

### **1. Trigger Release**
When code is merged to `main` branch:
```bash
git checkout develop
git pull origin develop
git checkout -b release/v1.0.0
# Update version in package.json
git add package.json
git commit -m "chore: bump version to 1.0.0"
git push origin release/v1.0.0
# Create PR from develop to main
```

### **2. Automatic Builds**
The workflow will automatically:
1. **Build Android APK** on Ubuntu
2. **Build iOS** on macOS
3. **Deploy Web** to Vercel
4. **Create GitHub Release** with proper tagging

### **3. Release Creation**
- **Tag Name**: `v{version}` (e.g., `v1.0.0`)
- **Release Name**: `Release v{version}`
- **Assets Attached**:
  - `app-release-{version}.apk`
  - `ios-build-{version}.zip`
- **Release Notes**: Auto-generated with commit history

## 📋 **Example Release**

When you release version `1.0.0`, you'll get:

### **GitHub Release Page**
```
Release v1.0.0
Tag: v1.0.0

📥 Assets:
├── app-release-1.0.0.apk (Android APK)
└── ios-build-1.0.0.zip (iOS Build)

📋 Release Notes:
├── 🚀 What's New
├── 📱 Mobile Apps
├── 🌐 Web App
├── 📋 Changes (commit history)
├── 📥 Downloads
└── 🔧 Technical Details
```

### **Download Links**
- **Android**: Direct download from GitHub release
- **iOS**: Download for TestFlight/App Store
- **Web**: Live at your Vercel domain

## 🏷️ **Version Management**

### **Version Format**
- Uses semantic versioning: `MAJOR.MINOR.PATCH`
- Version is read from `package.json`
- Tag format: `v{version}`

### **Example Versions**
```
v1.0.0 - Initial release
v1.0.1 - Bug fix
v1.1.0 - New feature
v2.0.0 - Breaking changes
```

## 🔧 **Technical Details**

### **Build Process**
1. **Android**: Expo build → APK → GitHub Release Asset
2. **iOS**: Expo build → Archive → GitHub Release Asset
3. **Web**: Expo export → Vercel deployment

### **Asset Naming**
- Android: `app-release-{version}.apk`
- iOS: `ios-build-{version}.zip`
- All assets are properly versioned

### **Release Notes Generation**
- Auto-generated from commit history
- Includes all commits since last release
- Professional formatting with emojis
- Technical details included

## ✅ **What You Get**

### **For Each Release:**
1. **GitHub Release** with proper tag
2. **Android APK** attached and downloadable
3. **iOS Build** attached for distribution
4. **Web App** deployed to Vercel
5. **Release Notes** with commit history
6. **Version Tagging** for all assets

### **Download Experience:**
- Users can download APK directly from GitHub
- iOS build available for TestFlight/App Store
- Web app live and accessible
- All assets properly versioned

## 🚀 **Getting Started**

1. **Set up GitHub Secrets** (see `SETUP_GITHUB_CI_CD.md`)
2. **Configure branch protection** rules
3. **Update version** in `package.json`
4. **Create PR** from `develop` to `main`
5. **Merge to main** triggers automatic release
6. **Download assets** from GitHub release page

The release process is fully automated and will create professional releases with all assets properly tagged and attached! 