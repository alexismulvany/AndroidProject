# (Name TBD): Rock Climbing Companion App

## Project Overview
(Name TBD) is a mobile-first Android application designed specifically for rock climbers. It leverages Android's unique mobile capabilities to provide an infinite "doomscrolling" feed of climbing routes and utilizes hardware sensors (Accelerometer, Barometer, GPS) to track climbing sessions passively.

## Core Requirements Addressed
1. **Doomscrolling:** Infinite vertical scroll of climbing routes utilizing the Boardsesh/BoardLib SQLite databases.
2. **Mobile Sensors:** 
   - **Accelerometer & Barometer:** Auto-logs climbing attempts, wall-time, and falls.
   - **GPS / Geofencing:** Filters the feed based on the user's physical presence at a specific climbing gym.

---

### Sensor & Background Services Layer
*   **Foreground Service:** Since climbing sessions can last hours and the phone will be locked in a pocket, a Foreground Service (with an ongoing notification) is required to keep the `SensorManager` running without Android killing the process.
*   **SensorManager:** Will listen to `TYPE_LINEAR_ACCELERATION` and `TYPE_PRESSURE`.
*   **FusedLocationProviderClient:** Used for one-off or periodic checks to determine the closest gym for the geofencing feature.

---

## Tech Stack
*   **Language:** Kotlin
*   **Asynchronous Programming:** Kotlin Coroutines & Flow
*   **Sensors:** Android `SensorManager`, Google Play Services Location API
