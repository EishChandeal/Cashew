# Cashew

A beautifully designed personal finance and budget tracking application. 

This repository contains my customized version of the Cashew app, featuring bug fixes, dependency updates for modern Flutter environments, and UX improvements (like a streamlined, reversed transaction entry flow).

## Getting Started

Follow these instructions to build and test the app on your Android device or emulator.

### Prerequisites

1. **Flutter SDK**: Install the [Flutter SDK](https://docs.flutter.dev/get-started/install) for your operating system.
2. **Android Studio**: Install [Android Studio](https://developer.android.com/studio) to get the necessary Android SDKs and build tools.
3. **Android Device**: 
   - **Physical Device**: Enable [Developer Options and USB Debugging](https://developer.android.com/studio/debug/dev-options) on your Android phone and connect it to your computer via USB.
   - **Emulator**: Alternatively, set up an Android Virtual Device (AVD) through Android Studio.

### Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/EishChandeal/Cashew.git
   ```

2. **Navigate to the Flutter project directory:**
   The actual Flutter application code is located inside the `budget` folder.
   ```bash
   cd Cashew/budget
   ```

3. **Install dependencies:**
   ```bash
   flutter pub get
   ```

4. **Run the app:**
   Make sure your Android device is connected (or your emulator is running), then execute:
   ```bash
   flutter run
   ```
   *If you have multiple devices connected (like Chrome and an Android phone), Flutter will prompt you to select one. You can bypass this by specifying the device, e.g., `flutter run -d android`.*

### Building an APK (For Android)

If you want to build a standalone APK file that you can share or install permanently on your device without keeping it connected to your computer:

```bash
flutter build apk --release
```
Once the build finishes, you can find the generated APK file at:
`budget/build/app/outputs/flutter-apk/app-release.apk`
