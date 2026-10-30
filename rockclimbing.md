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

*   ---

## API & Data Integration

### 1. BoardLib (Python Utility)
*   **Description:** An open-source Python library designed to interact with the undocumented APIs of major climbing boards (like Kilter, Tension, and Grasshopper) managed by Aurora Climbing. 
*   **Key Features:** It bypasses the need to scrape data by directly downloading the complete, synchronized `.sqlite` database of every public climb and its metadata (grade, setter, angle, hold placements).
*   **How we use it:** We will not run this on the phone. Instead, we use BoardLib on a developer machine to fetch the official `.sqlite` databases. We then bundle these pre-populated database files directly into the Android app's `assets` folder. This allows our app to use Android's Room database to query the data locally, enabling blazing-fast infinite scrolling without network latency or API rate limits.

### 2. Boardsesh (Reference / Alternative API)
*   **Description:** Boardsesh is a free, open-source community app that acts as a unified platform for all climbing boards. 
*   **Key Features:** It reverse-engineers the Bluetooth protocols to light up physical boards, manages user logbooks, and supports custom "spray walls" using computer vision on photos.
*   **How we use it:** While BoardLib provides our raw data, the Boardsesh open-source repository serves as our architectural reference. If we decide to add Bluetooth LED integration in the future (allowing users to light up the board directly from our app's feed), we will utilize Boardsesh's open-source Bluetooth logic rather than writing it from scratch.

### 3. Google Play Services Location API (FusedLocationProviderClient)
*   **Description:** Android's recommended, battery-efficient framework for handling device location and geofencing.
*   **Key Features:** It intelligently combines GPS, Wi-Fi, and cellular networks to determine the user's location while minimizing battery drain—crucial for an app running in a climber's pocket for hours.
*   **How we use it:** We use the `GeofencingApi` to draw invisible boundaries around the user's favorite climbing gyms. When the Fused Location Provider detects the phone has entered the gym, it triggers a background event that automatically filters the doomscrolling feed to only show climbs available at that specific gym's board angle and setup.
