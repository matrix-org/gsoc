---
name: Nheko VOIP Library
desc: Refactor the VOIP support in Nheko into a reusable library and update it to VOIP v1.
# add a short one line description of your project
requirements:
# Student requirements:
 - Knowledge of C++.
 - Familarity with WebRTC is beneficial.
 - Some Qml will be used but can be learned on the go.
difficulty: medium
issues:
# Related issues (if any)  to this project.
 - No main issue, but some are related to some VOIP features.
 - https://github.com/Nheko-Reborn/nheko/labels/voip
mentors:
# First person in contact; mentors may change before project starts.
 - Nico (@deepbluev7:neko.dev)
initiatives:
 - GSoC
tags:
# Different technologies needed
 - C++
 - WebRTC
---

#### Description

[Nheko is a desktop (and mobile) client for the Matrix
protocol](https://github.com/Nheko-Reborn/nheko/).
It intends to be fast, not get in your way, use few resources, but be as
powerful as you need it to be.

Nheko already supports voice and video calls, but currently this code can not be
reused in other clients and it doesn't support the latest updates to the Matrix
VOIP protocol. It would be great to update the code to enable new features like
muting, mixing multiple streams, group conferences and make the calls more
reliable and faster.

You won't have to do all of the above. Pick what you prefer to do and fits
inside your schedule. Group calls would be awesome, but are also a lot harder to
add. Refactoring the code to be a library is probably required to have a clean
interface. Some of the advanced features might not be necessary for a desktop
client like Nheko.

You can find the full list of MSC using the voip label on the matrix-doc repo:
https://github.com/matrix-org/matrix-doc/pulls?q=is%3Apr+is%3Aopen+label%3Avoip

The suggested milestones are a bit bottom heavy. You may want to move some of
the later parts a bit earlier once you decided on your flashy projects finale.

#### Milestones

##### GSOC CODING STARTS

* Get familiar with the Nheko codebase.
* Do a few calls.
* Update [mtxclient](https://github.com/Nheko-Reborn/mtxclient) to support the
    new voip version from [MSC2746](https://github.com/matrix-org/matrix-doc/pull/2746).
* Add support for the types you expect to need for your flashy project(s) in the
    final period.

##### GSOC MIDTERM

* Update Nheko to support the new voip types.
* Implement trickle ICE support.
* Define a library interface and move the voip code into a separate CMake
    project.
* Improve stats output and debug logging.
* Prepare integration for some parts of your flashy project(s).

##### GSOC FINAL

* Finish by adding something flashy. This could be something or multiple things
    from the following list:
  - Support calling yourself. (est. 1.5 weeks)
  - Support transfering a call. (est. 2 weeks)
  - Support sending DTMF in calls. (est. 2 weeks)
  - Support connecting to a SIP bridge. (est. 3 weeks)
  - Support basic group call signaling. (est. 6 weeks)
  - Enable VOIP support on macOS and/or Windows. (est. 2 weeks)
  - Support screensharing on Wayland (and/or other platforms). (est. 2 weeks)
  - Support noise cancellation. (est. 1 week)
  - Port the gstreamer qmlsink to qt6. (needs basic Vulkan, OpenGL and maybe other
      Graphic library skills) (est. 4 weeks)
