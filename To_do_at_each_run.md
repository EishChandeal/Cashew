## Running the App Locally (Android Emulator & Physical Devices)

If you are setting up this project for the first time, here is how you can run the app on Android:

### Prerequisites
1. Ensure you have the Android SDK and Flutter SDK installed and configured.
2. Open your terminal and **navigate to the `budget` directory** (the actual Flutter project is inside it):
   ```bash
   cd budget
   ```
3. Get the project dependencies:
   ```bash
   flutter pub get
   ```

### 1. Running on an Android Emulator
1. Open Android Studio and launch an Android Virtual Device (AVD) from the Device Manager.
2. Wait for the emulator to fully boot up to the home screen.
3. Verify the emulator is recognized by Flutter by running:
   ```bash
   flutter devices
   ```
4. Run the app:
   ```bash
   flutter run
   ```
   *(If you have multiple devices connected, the terminal will list them and ask you to type a number to select the emulator. Alternatively, run `flutter run -d <device_id>`)*

### 2. Running on a Physical Android Device
1. On your Android phone, go to **Settings > About Phone** and tap the **Build Number** 7 times to enable Developer Options.
2. Go back to **Settings > System > Developer Options** and enable **USB Debugging**.
3. Connect your phone to your computer via a USB cable. 
   - *Note: A prompt will appear on your phone asking to "Allow USB debugging". Check "Always allow from this computer" and tap OK.*
4. Verify your physical device is recognized:
   ```bash
   flutter devices
   ```
5. Run the app:
   ```bash
   flutter run
   ```

---

## If the app doesn't run after your first run

When you stop the app after its first run in Windows OS:

There is an annoying Windows-specific Flutter quirk. It usually happens when a file in the `build/` or `.dart_tool/` folder gets "locked" by another process (like your IDE indexing, or a background dart process). 

To fix this permission error, run these two commands before trying to run the app again (at each re-run basically):

```bash
flutter clean
flutter pub get
```

After doing that, `flutter run -d chrome` should successfully launch the app!

## To stop this permanently:

Here are the 3 most common culprits and how to fix them permanently:

### 1. The #1 Offender: Windows Defender (Antivirus)
Windows Defender loves to scan new files the exact millisecond they are created. When Flutter compiles your app, it creates thousands of files very quickly. Defender scans them, locks them, and causes Flutter to crash with a "permission error."

**The Permanent Fix:** Add your project folder and Flutter SDK to Windows Defender Exclusions.
1. Open the Windows Start menu and type **Windows Security**.
2. Click **Virus & threat protection**.
3. Under "Virus & threat protection settings," click **Manage settings**.
4. Scroll down to the "Exclusions" section and click **Add or remove exclusions**.
5. Click **Add an exclusion** -> **Folder**.
6. Select your Cashew project folder (`C:\Users\HP\Desktop\products_mobo\money_things\Cashew`).
7. *(Highly Recommended)* Do it again and select your Flutter SDK installation folder (e.g., `D:\flutter` or wherever it's installed).

### 2. Zombie Dart Processes
Sometimes when you close an emulator or cancel a build with `Ctrl+C`, the background `dart.exe` process doesn't fully close. The next time you run `flutter run`, it trips over the ghost process that is still holding onto the files.

**The Fix:** If it happens again, instead of restarting your whole computer, you can force-kill all stuck Dart processes. Just run this command in your PowerShell:
```powershell
taskkill /F /IM dart.exe
```

### 3. IDE File Indexing (VS Code / Android Studio)
Your IDE is constantly trying to "read" your files to provide autocomplete and error highlighting. If it tries to read the `build/` folder while Flutter is modifying it, it can cause a lock.

**The Fix:** Make sure your IDE isn't trying to index the build folders. In the Cashew project, there is already a `.gitignore` which helps, but if you are using VS Code, you can add this to your `.vscode/settings.json` to tell the IDE to ignore the build folder completely:
```json
{
    "files.exclude": {
        "**/build": true,
        "**/.dart_tool": true
    },
    "search.exclude": {
        "**/build": true,
        "**/.dart_tool": true
    }
}
```

**To summarize:** Add the folder exclusion to Windows Defender first. That solves this problem permanently for 90% of Windows Flutter developers. If it ever pops up again randomly, use the `taskkill` command to clear the ghost processes