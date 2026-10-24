# Prawko Android

[![CI](https://github.com/Laska254/prawko-android/actions/workflows/ci.yml/badge.svg)](https://github.com/Laska254/prawko-android/actions/workflows/ci.yml)

## Table of Contents

* [Table of Contents](#table-of-contents)
* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
    + [Code style](#code-style)
    + [Dependency updates](#dependency-updates)
* [Usage](#usage)

---

## Overview

**Prawko Android** is an Android client created with Kotlin, Jetpack Compose and Material 3 for Prawko projects.

It is the Android client for [Prawko Server](https://github.com/Laska254/prawko-server) and aims to use its whole REST
API. All data and authentication are handled by the server, so it must be running for the app to work.

---

## Prerequisites

* [Android Studio](https://developer.android.com/studio) (includes the Android SDK and a JDK)
* Android device or emulator with Android 7.0 (API 24) or newer
* Running [Prawko Server](https://github.com/Laska254/prawko-server)
* JDK 21 - only to build from the terminal

Gradle doesn't have to be installed - the repository includes the Gradle Wrapper (`./gradlew`, `gradlew.bat` on
Windows). The Gradle daemon runs on JDK 25, which Gradle downloads automatically on the first build.

### Debian 13

Download Android Studio from [developer.android.com/studio](https://developer.android.com/studio), extract it and run
`bin/studio.sh`.

`sudo apt install openjdk-21-jdk`

The emulator needs KVM for hardware acceleration. Add yourself to the `kvm` group and log out and back in:

`sudo usermod -aG kvm $USER`

### Windows

`winget install Google.AndroidStudio`

`winget install Microsoft.OpenJDK.21`

---

## Installation

Run Prawko Server first. You can find instructions in
its [README](https://github.com/Laska254/prawko-server/blob/main/README.md).

Clone repository

`git clone https://github.com/Laska254/prawko-android.git`

`cd prawko-android`

Open the project in Android Studio and wait for the Gradle sync, then run the `app` configuration. Or use the terminal:

Build (APK in `app/build/outputs/apk/debug/`)

`./gradlew assembleDebug`

Install on a connected device or emulator

`./gradlew installDebug`

Unit tests

`./gradlew test`

Instrumented tests (requires a connected device or emulator)

`./gradlew connectedAndroidTest`

Android lint (report in `app/build/reports/`; any warning fails the build, version checks for dependencies, AGP and `targetSdk` are informational only)

`./gradlew lint`

### Code style

Kotlin code is formatted with [ktlint](https://pinterest.github.io/ktlint/) (Android Studio style)
and [Compose rules](https://mrmans0n.github.io/compose-rules/), run by [Spotless](https://github.com/diffplug/spotless).
Rules are configured in `.editorconfig`.

Format code

`./gradlew spotlessApply`

Check formatting (run in CI)

`./gradlew spotlessCheck`

### Dependency updates

[Dependabot](https://docs.github.com/en/code-security/dependabot) checks for updates weekly and opens pull requests
labelled `dependencies`:

* Gradle - the version catalog (`gradle/libs.versions.toml`), settings plugins and the Gradle Wrapper. AndroidX and
  Compose, AGP and Kotlin, test libraries, and code style tools (Spotless, ktlint, Compose rules) are each grouped into
  one pull request.
* GitHub Actions - all actions in `.github/workflows/` in one pull request.

Releases younger than 7 days are skipped. Configuration: `.github/dependabot.yml`. `compileSdk`, `targetSdk` and the
Gradle daemon JDK (`gradle/gradle-daemon-jvm.properties`) are not covered and are updated by hand.

---

## Usage

Server URL: not configured yet.

When Prawko Server runs on your computer:

* emulator - `http://10.0.2.2:8080/` (the emulator's alias for the computer's `localhost`)
* physical device - `http://<computer's LAN IP>:8080/`, both on the same network

Unlike Prawko Web, the app is not subject to CORS, so the server needs no extra configuration for it.
