---
name: reactions and edits for Nheko
desc: Add support for reaction to and editing messages via Nheko.
requirements:
 - C++, some understanding of lambdas and C++17's std::variant will be beneficial
 - Qt, mainly Qml
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
library as in the backend, which is based on Boost.Asio and Boost.Beast. Nheko does support E2EE and other advanced matrix features. Riot and some other clients recently added
reactions and edits, which are cool features based on [MSC1849](https://github.com/matrix-org/matrix-doc/pull/1849). Both of those would be nice to have in Nheko and it would also
solve the issues of not seeing some events at all (reactions) or being spammed with overly long messages, that are almost an exact repetition of the one before it (edits).

#### Contacts

You can reach the mentors for questions via Matrix in the #nheko-reborn:matrix.org room or directly:
- Nico (@deepbluev7:neko.dev)
- red_sky (@red_sky:ocean.joedonofry.com)

#### Milestones

##### Before GSOC

* Read the current [MSC for relations](https://github.com/matrix-org/matrix-doc/pull/1849) and try them out in a different client (like Riot). You can even inspect the events to get
    an idea of how they look and work in practice.
* Join #nheko-reborn:matrix.org and get to know the contributors and community.
* Clone the [nheko repo](https://github.com/Nheko-Reborn/nheko/) and compile the current dev branch.
* Maybe you can find something small to contribute to get familiar with the code, development and the contribution process. There is probably a typo or a bad ui layout somewhere in the
    code.

##### GSOC CODING STARTS

* Implement reaction events in mtxclient for sending and receiving them. Don't forget to add tests!
* Implement a way to display them in the timeline (adapt the message delegates, probably via a Qml repeater).
* Extend the timeline model to include reactions.
* It should now be possible to see reactions from other clients in Nheko.

##### GSOC MIDTERM

* Using your experience of the timeline model and mtxclient, extend the abstractions in mtxclient to support edited events.
* Implement the necessary changes to send and receive edits in mtxclient (and add unit tests again).
* Extend the timeline model to contain and render edits properly. Maybe this can even support an edit history?

##### GSOC FINAL

* Enable increasing/decreasing the reaction count and adding your own new reactions.
* Implement a way to edit a message, that was sent by the user, in Nheko.
* Stretch goal: Add a way to display all the edits done to a message (edit history).
