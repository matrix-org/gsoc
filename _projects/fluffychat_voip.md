---
name: FluffyChat webrtc
desc: Make webrtc support in FluffyChat ready for daily use
requirements:
 - Familiar with Dart/Flutter
difficulty: high
issues:
 - https://gitlab.com/famedly/fluffychat/-/issues/874
mentors:
 - Krille
initiatives:
 - GSoC
tags:
 - Flutter
 - Dart
 - WebRTC
---

#### Description

Videocalls are implemented but very experimental. They crash a lot and the error handling is not perfect.

Tasks:

- The app crashes sometimes on incoming calls
- The app should ring when there is an incoming call, even when the app is in background or terminated
- The app should give an audio feedback on starting and ending a call
- Errors should be displayed better if something goes wrong

This needs a lot of low level knowledge about Flutter, Dart, WebRTC and the used libraries.

#### Milestones

##### GSOC CODING STARTS

* The student got used to the codebase of FluffyChat and the Dart Matrix SDK
* Sound effects are already working

##### GSOC MIDTERM

* Video Calls are no longer crashing the app

##### GSOC FINAL

* Video Calls are stable now
* Ringing on Android works even when the app is in background or terminated
