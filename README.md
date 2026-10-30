# HoneyAnim

LSPosed module for One UI Home (`com.sec.android.app.launcher`) that overrides the app open/close
transition parameters of `com.honeyspace.transition`.

## Build
1. Put `api-82.jar` (legacy Xposed API) in `app/libs/`.
2. Open in Android Studio (or `gradle assembleRelease`), install the APK.
3. LSPosed -> Modules -> enable HoneyAnim, scope = Launcher (already suggested), force-stop launcher.

## What gets hooked
`data.open.{HighEnd,LowEnd,LowestEnd,HomeUp}OpenParams` and `data.close.{...}CloseParams` getters.
Stock High-End values (from the decompile):

| Open                 | Stock                              |
|----------------------|------------------------------------|
| window position      | 650 ms, bezier (0.2, 0.94, 0.05, 1)|
| window alpha         | 250 ms                             |
| wallpaper            | 800 ms, scale 1.3                  |
| home layer           | 800 ms, scale 0.85                 |
| task window position | 350 ms, bezier (0.33, 0, 0.2, 1)   |

| Close                | Stock                              |
|----------------------|------------------------------------|
| window/wallpaper/content/alpha | 350 ms each              |
| no-target alpha      | 250 ms                             |

Add more overrides in `Hook.java`: put the getter name into one of the maps / `isHandled`.
Logs: LSPosed -> Logs, look for `HoneyAnim:`.
