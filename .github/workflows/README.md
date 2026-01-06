# GitHub Actions Workflows

This directory contains GitHub Actions workflows for automating the build and release process of the Beerus Framework.

## Workflows

### 1. Build APK and Magisk Module (`build.yml`)

This workflow automatically builds both the APK and Magisk module on every push and pull request to the main/master branch.

**Triggers:**
- Push to `main` or `master` branch
- Pull requests to `main` or `master` branch
- Manual trigger via GitHub Actions UI

**What it does:**
1. Sets up Java 17 and Android SDK/NDK
2. Builds the Beerus Framework APK (includes Frida Core and DB Agent)
3. Creates a standalone Magisk module ZIP
4. Uploads both artifacts for download

**Artifacts:**
- `beerus-apk`: The compiled Android APK
- `beerus-magisk-module`: The packaged Magisk module

### 2. Create Release (`release.yml`)

This workflow creates a GitHub release with the built APK and Magisk module.

**Triggers:**
- Push of a tag matching `v*` (e.g., `v1.0.0`, `v2.1.0`)
- Manual trigger via GitHub Actions UI (allows custom tag name)

**What it does:**
1. Builds both the APK and Magisk module
2. Creates a GitHub release with the specified tag
3. Attaches the APK and Magisk module to the release

**Usage:**
```bash
# Create a new release
git tag v1.0.0
git push origin v1.0.0
```

Or use the "Run workflow" button in GitHub Actions UI to manually trigger a release.

## Requirements

The workflows automatically install:
- JDK 17 (Temurin distribution)
- Android SDK
- Android NDK (version 26.1.10909125)

No additional setup is required in the repository settings.

## Customization

If you need to modify the NDK version, update the version in both workflow files:
```yaml
echo "y" | sdkmanager --install "ndk;26.1.10909125"
```

To change the Java version, update:
```yaml
java-version: '17'
```
