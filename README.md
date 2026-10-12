# The Narrow Way — Android app

A pixel-art choose-your-own-adventure through the Scriptures. The whole game is one
HTML file in `app/src/main/assets/index.html`, wrapped in a native Android WebView.
No game engine, no libraries, no internet needed to play.

---

## Build the APK without installing anything (recommended)

You need a free GitHub account. That's it. No Android Studio, no Java, no Mac.

1. Go to **github.com/new** and create a repository. Name it `the-narrow-way`.
   Set it to Private if you like — this works either way.
2. On the new repo's page click **uploading an existing file**.
3. Unzip this folder on your computer, then drag **everything inside it**
   (the `app` folder, the `.github` folder, `build.gradle`, `settings.gradle`,
   `gradle.properties`) into the upload box. Click **Commit changes**.
4. Click the **Actions** tab at the top. A job called **Build APK** starts by itself.
   Wait about 3-5 minutes for the green check.
5. Click into that finished run and scroll to **Artifacts** at the bottom.
   Download **TheNarrowWay-apk**. Inside the zip is `app-debug.apk`.

That file is your app.

> If the `.github` folder doesn't appear when you drag it, your computer is hiding
> folders that start with a dot. On Windows press `Ctrl+H` in File Explorer; on Mac
> press `Cmd+Shift+.` in Finder. Then drag it again.

## Build it locally instead

If you do have Android Studio: **File > Open**, pick this folder, wait for it to sync,
then **Build > Build Bundle(s)/APK(s) > Build APK(s)**.

From a terminal with the Android SDK installed: `gradle assembleDebug`
The APK lands in `app/build/outputs/apk/debug/`.

---

## Installing it on your friends' phones

Send them `app-debug.apk` over WhatsApp, Telegram, Google Drive, or a USB cable.
When they tap it, Android will warn that it's from an unknown source — that warning is
normal for any app not downloaded from the Play Store. They tap **Settings** on the
prompt, allow installs from whichever app they received it through, then tap the file
again and **Install**.

This APK is signed with the standard Android debug key, which is fine for sharing with
friends. You only need a real signing key if you ever want to publish on the Play Store.

## Changing the game

Everything lives in `app/src/main/assets/index.html` — all the story text, the choices,
the pixel art, and the sound. Edit that one file, push it to GitHub, and the Actions tab
builds you a fresh APK automatically.

The story nodes are the `N.xxx = {...}` entries. Each has `text`, an optional `verse`,
and a list of `choices`, where every choice has `t` (the words on the button), `fx`
(which stats move), an optional `mark`, and `to` (the next node's id).

## Notes

- The two display fonts load from Google Fonts, so with no internet the app falls back
  to the phone's built-in monospace and serif. The game is fully playable offline either
  way; only the lettering changes.
- Sound is generated live by the Web Audio API — there are no audio files to ship.
- Your run is saved on the phone, so closing the app doesn't lose your place.
- `minSdk 26` means Android 8.0 and newer, which covers almost every phone in use.
