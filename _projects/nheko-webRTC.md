---
name: WebRTC support for Nheko
desc: Add WebRTC based audio and/or video chat suport to Nheko.
requirements:
 - C++
 - C
 - Qt, mainly Qml
difficulty: high
issues:
 - https://github.com/Nheko-Reborn/nheko/issues/109
mentors:
 - deepbluev7
 - redsky17
initiatives:
 - GSOC
tags:
 - C++
 - GUI
collaborating_projects:
 - Nheko
---

#### Description

Nheko is a native Matrix client written in C++ using the Qt toolkit using a mix of Qt Widgets and Qml. It uses the [mtxclient](https://github.com/Nheko-Reborn/mtxclient) Matrix
library as in the backend, which is based on Boost.Asio and Boost.Beast. Nheko does support E2EE and other advanced matrix features. One of the big features still missing is support
for Voip/WebRTC to do Video/Voice calls. As far as I'm aware, there is no native desktop client, that supports this, yet.

As a moonshot of a proposal, it would be cool to add such capabilities to Nheko. This is a complicated project, so limiting what actually gets implemented is reasonable. For example
it would be totally fine to only implement only Voice calls, only implement accepting calls from more full featured clients like Riot/Web or only implement support for it on one of
Nheko's supported platforms (i.e. Linux). In every case care should be taken, that the implementation is eventually extensible to provide all the features one would expect from Voice
and Video chats (1:1) after the GSOC. Success criteria will probably be a successful call (Voice or Video), which includes at least one participating Nheko client, where at least one
side can receive Audio or Video.

Some pointers, which may be helpful:
- We don't aim to include QtWebengine to do WebRTC, since it is a very heavy dependency.
- Gstreamer added support for WebRTC in version 1.14. Some examples on how that works can be found [here](https://github.com/centricular/gstwebrtc-demos).
- Gstreamer output can be used in a QtApplication via [qmlsink](https://github.com/GStreamer/gst-plugins-good/tree/master/tests/examples/qt/qmlsink).
- The Matrix spec for calls can be found [here](https://matrix.org/docs/spec/client_server/latest#voice-over-ip).

#### Contacts

You can reach the mentors for questions via Matrix in the #nheko-reborn:matrix.org room or directly:
- Nico (@deepbluev7:neko.dev)
- red_sky (@red_sky:ocean.joedonofry.com)

#### Milestones

These are only guidelines. They should be adapted as needed to increase chances to have a successful project

##### Before GSOC

* Read up on WebRTC and how Matrix uses it. Maybe try out doing a call with Riot/Web or Riot/Desktop.
* Scour the web for WebRTC documentation/examples using Gstreamer (or an alternative library, if you think there is a better one).
* Join #nheko-reborn:matrix.org and get to know the contributors and community.
* Clone the [nheko repo](https://github.com/Nheko-Reborn/nheko/) and compile the current dev branch.
* Maybe you can find something small to contribute to get familiar with the code, development and the contribution process. There is probably a typo or a bad ui layout somewhere in the
    code.
* Consider if it can be done. Maybe reprioritize to some other contribution to Nheko, if you think it will be too complicated.

##### GSOC CODING STARTS

* Implement a basic example application, that uses qmlsink to show a WebRTC stream. You can probably use an existing demo for that and replace the window with a Qml window.
* Figure out how it does connection negotiation and how that can be related to how Matrix does it.
* Start implementing the event types for call negotiation in mtxclient.

##### GSOC MIDTERM

* Integrate the Qml sink into Nheko as a separate window or into the main window.
* Implement call setup in Nheko using the event types in mtxclient. You probably want to enable rendering those event types in the timeline and add a command or button to act on them.
* Start integrating call setup and gstreamer. You should be seeing some light at the end of the tunnel approaching the end of this milestone on how to approach finalizing this
    project.

##### GSOC FINAL

* Finalize your implementation, so that you can either accept or initiate a call and have something visible and/or audible to show.
* This milestone will probably be mostly be composed of working out the kinks in the implementation.
* Stretch goal: Support for turn servers, to travers NATs.
