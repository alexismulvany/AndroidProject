# AndroidProject

Early planning repository for a collaborative Android app project (Kotlin + Groovy Gradle).

## Current Status

We are intentionally keeping starter code minimal while finalizing the idea.

Planned stack:
- Android app
- Kotlin
- Gradle with Groovy build scripts

## Product Idea

**The Pitch:**  
An infinite vertical feed for gaming friend groups that solves *"What should we play tonight?"* while delivering friend leaderboards, backlog roasts, and trending gaming media.

## Key App Features

### 1) The Co-Op Matchmaker & Overlap Engine
- **One-Tap Friend Sync:** Log in via Steam OpenID and automatically fetch the user's friends list (no manual 64-bit Steam ID entry).
- **Multi-Friend Overlap:** Select 2 to 8 friends from an interactive avatar list and calculate the intersection of everyone’s owned games.
- **Roulette Wheel:** Spin a decision wheel filtered by genre, co-op tags, or play history to pick tonight’s game.

### 2) The Doomscrollable Feed (Cards)
Users swipe vertically through a dynamic feed combining friend activity and discovery:

- **Co-Op Overlap Cards:**  
  Example: *"3 of you own Deep Rock Galactic, but 0 have played it this month."*

- **Friend Leaderboard & "Wall of Shame" Cards:**
  - **The Backlog Hoarder:** Ranks friends by total dollar value of unplayed games.
  - **The Night Owl:** Highlights friends playing past 2 AM.
  - **The Abandoner:** Displays games bought, played for under 30 minutes, and dropped.

- **Game Discovery Cards:**
  - **"Is It Dead?" Metrics:** Current vs. peak player counts with drop-off charts.
  - **Community Roasts:** Funny or scathing community reviews fetched via the Steam Storefront API.
  - **Gameplay Trailers:** 10-second autoplaying clips (via YouTube Shorts / Twitch Clips API).

## Collaboration Notes

- This repository is intended for three collaborators.
- Keep changes small and reviewable while the concept is evolving.
- Avoid heavy scaffolding until requirements are locked.

## Suggested Next Setup (When Ready)

When the concept is finalized, add:
- Android Studio project scaffold with Kotlin support
- Groovy-based Gradle files (`settings.gradle`, root `build.gradle`, app `build.gradle`)
- Basic package naming convention and module structure
- CI checks for build + unit tests
