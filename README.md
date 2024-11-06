This is the backup of the last stable version of **Battery Charge Limit** that is known to work as intended on Android 13 and LineageOS 20.0 (unlike the [fork by MuntashirAkon](https://github.com/MuntashirAkon/BatteryChargeLimiter)). For whatever reason this version was unfortunately removed from [F-Droid](https://f-droid.org) altogether with a whole lot of other "outdated" apps and it is not available from [IzzyOnDroid](https://apt.izzysoft.de/fdroid/) either.

The [APK](https://github.com/Efenstor/BatteryChargeLimit/releases) in the releases is the backup I made from my own phone using [SAI](https://github.com/Aefyr/SAI).

---

# BatteryChargeLimit
Source code of the android app that stops charging at a desired level. ***Requires root.***

For more info: https://forum.xda-developers.com/android/apps-games/root-battery-charge-limit-t3557002

[<img src="https://f-droid.org/badge/get-it-on.png"
     alt="Get it on F-Droid"
     height="80">](https://f-droid.org/packages/com.slash.batterychargelimit/)
[<img src="https://play.google.com/intl/en_us/badges/images/generic/en-play-badge.png"
     alt="Get it on Google Play"
     height="80">](https://play.google.com/store/apps/details?id=com.slash.batterychargelimit)

Since version 0.7, the charging limit can be set using Intents. There are two ways for doing so:
- Using an Intent to Broadcast a message of action *"com.slash.batterychargelimit.CHANGE_LIMIT"*, supplying the percentage by the *Intent extra "android.intent.extra.TEXT"* (Intent.EXTRA_TEXT). For example in Tasker, the extra could look like *android.intent.extra.TEXT:80* to set the limit to 80%. __This is technically more clean and therefore recommended!__
- Starting Activity *com.slash.batterychargelimit.LimitChangeActivity* with a *ACTION_SEND* intent, using *MIME type "text/x-battery-limit"* and supplying the percentage as String with *Intent extra "android.intent.extra.TEXT"* (Intent.EXTRA_TEXT). __This will cause the receiving Activity to pop up for a short moment. The Intent should be provided with FLAG_ACTIVITY_NO_HISTORY, otherwise the main activity of this app will become the foreground Activity after sending the Intent.__

## Troubleshooting
1. Many Samsung phones do not support the default "/sys/class/power_supply/battery/charging_enabled" control file, so I recommend to go to the *Settings > Set Control File* and select either "batt_slate_mode" or "store_mode" (may work better for newer phones).
2. In case you selected the "store_mode" control file it is also recommended to enable "Always Handle Power Events" in the "Advanced Settings" section.
3. It is also recommended to enable the "Always Write CTRL File" option, especially if you experience the situation when the phone is connected to the charger but does not charge at all and the status in the app always says "DISCHARGE", although the notification appears and disappears correctly.
