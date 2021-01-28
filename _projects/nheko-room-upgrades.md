---
name: Room Upgrade Support for Nheko
desc: Implement a visually pleasing way to handle upgraded rooms and upgrade rooms in Nheko.
requirements:
 - C++, some understanding of lambdas and C++17's std::variant will be beneficial
 - Qt, mainly Qml and Models
difficulty: medium
issues:
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
library as in the backend, which is based on Boost.Asio and Boost.Beast. Nheko does support E2EE and other advanced matrix features.

Rooms in Matrix are distributed over multiple servers. To handle such a heterogenous server infrastructure, rooms have a version. This specifies how a server should handle certain
things regarding state resolution, default values and more. From time to time it may be necessary to upgrade a room to fix issues. This means, that the old room gets "thombstoned"
and should effectively be read only, while a new successor room is created, that inherits some of the old state and can be used to continue the conversation.

Currently both of those rooms are shown as regular rooms in nheko, which can be very confusing and disruptive. It would be preferable to show them as a single room, which can be
scrolled seamlessly. Nheko should make this experience as pleasant as possible. State resets or members leaving the old room shouldn't disrupt the new room for example. You should
also be possible to upgrade a room using Nheko.

#### Contacts

You can reach the mentors for questions via Matrix in the #nheko-reborn:matrix.org room or directly:
- red_sky (@red_sky:ocean.joedonofry.com)
- Nico (@deepbluev7:neko.dev)

#### Milestones

The milestones are just a general timeline, you may want to move some elements to a closer milestone to have more time for fixing bugs in the last few weeks, since time can be an
issue shortly before the deadline.

##### Before GSOC

* Get familiar with the concept of rooms, room versions and upgrades. The [spec for room upgrades may be helpful](https://matrix.org/docs/spec/client_server/latest#id160). Also ask
    around, what pitfalls others experience with room upgrades.
* Join #nheko-reborn:matrix.org and get to know the contributors and community.
* Clone the [nheko repo](https://github.com/Nheko-Reborn/nheko/) and compile the current dev branch.
* Maybe you can find something small to contribute to get familiar with the code, development and the contribution process. There is probably a typo or a bad ui layout somewhere in the
    code.

##### GSOC CODING STARTS

* Add the request for upgrading a room to mtxclient including unit tests.
* Implement upgrading a room, by adding a respective command or button to Nheko, probably in the room settings.
* Get familiar with the relation of room creation and thombstone events.

##### GSOC MIDTERM

* Extend the timeline to allow events from multiple rooms.
* Show a visual distinction where the break between the rooms is.
* Implement paginating old messages in a room, even over a room upgrade boundary.

##### GSOC FINAL

* Fix the remaining issues with room upgrades, so that all features work in upgraded rooms as usual.
* Consider allowing the user to invite old users, when upgrading invite only rooms.
* Make sure upgraded rooms don't appear twice in the room list
* Maybe use the cache more agressively for messages.
