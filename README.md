# AndroidProject

Early planning repository for a collaborative Android rock climbing companion app.

## Current Status

We are intentionally keeping starter code minimal while finalizing the idea.

Planned stack:
- Android app
- Kotlin
- Kotlin Coroutines and Flow
- Gradle with Groovy build scripts
- Android `SensorManager`
- Google Play Services Location API

## Product Idea

**The Pitch:**  
An infinite, mobile-first feed of climbing routes that helps climbers discover climbs, save routes to try, and passively track climbing sessions.

*  **Category:** Fitness
*  **Mobile:** Uses sensors to track height 
*  **Market:** Rock climbers
*  **Core habit:** Scroll through board climbs and save them for future sessions.
*  **Category:** Fitness

## Key App Features

### 1) Doomscrollable Climbing Feed

- Infinite vertical scrolling of climbing routes.
- Local route data queried from pre-populated BoardLib/Boardsesh SQLite databases.
- Route metadata such as grade, setter, angle, and hold placements.
- Save interesting climbs to try during a future session.

### 2) Passive Session Tracking

- Uses the phone’s accelerometer and barometer to track climbing sessions.
- Automatically logs attempts, wall time, and falls.
- Runs through an Android Foreground Service with an ongoing notification so sensors continue working while the phone is locked in a pocket.

### 3) Gym-Aware Discovery

- Uses `FusedLocationProviderClient` to identify the closest climbing gym.
- Uses geofencing to detect when a user enters a favorite gym.
- Filters the feed to climbs available at that gym’s board, angle, and setup.

## Data and API Integration

### BoardLib

BoardLib is an open-source Python utility that interacts with the undocumented APIs for major climbing boards, including Kilter, Tension, and Grasshopper. It downloads synchronized SQLite databases containing public climbs and metadata.

The app will not run BoardLib on the phone. Developers will use it to fetch official databases, bundle the pre-populated SQLite files in the Android app’s `assets` folder, and query them locally through Room. This supports fast feed scrolling without network latency or API rate limits.

### Boardsesh

Boardsesh is an open-source community app supporting multiple climbing boards, Bluetooth board control, logbooks, and spray walls. Its repository is an architectural reference for potential future Bluetooth LED integration, allowing the app to light routes directly on a physical board.

### Google Play Services Location API

`FusedLocationProviderClient` combines GPS, Wi-Fi, and cellular signals to provide battery-efficient location checks. The app will use it with geofencing to detect gym entry and automatically tailor route discovery to the user’s current gym.

## Sensor and Background Services

- **Foreground Service:** Keeps session tracking active for extended climbing sessions and displays an ongoing notification.
- **SensorManager:** Listens for `TYPE_LINEAR_ACCELERATION` and `TYPE_PRESSURE`.
- **FusedLocationProviderClient:** Performs one-off or periodic location checks for gym discovery and geofencing.

## Collaboration Notes

- This repository is intended for three collaborators.
- Keep changes small and reviewable while the concept is evolving.
- Avoid heavy scaffolding until requirements are locked.

## Suggested Next Setup (When Ready)

When the concept is finalized, add:
- Android Studio project scaffold with Kotlin support
- Groovy-based Gradle files (`settings.gradle`, root `build.gradle`, app `build.gradle`)
- Basic package naming convention and module structure
- Room entities and DAOs for the bundled climbing databases
- Foreground service and sensor tracking implementation
- Location permissions and gym geofencing
- CI checks for build + unit tests
