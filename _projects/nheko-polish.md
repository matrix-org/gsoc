---
name: Polish Nheko
desc: Add features and polish existing features, that make Nheko useable as someones/your primary client.
requirements:
 - C++, some understanding of lambdas and C++17's std::variant will be beneficial
 - Qt, mainly Qml and Models
difficulty: easy
issues:
mentors:
 - redsky17
 - deepbluev7
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

Nheko added a lot of big features recently, but it is missing a lot of smaller features, which makes people reach to Element, when they need them.
There are a lot of open issues for a lot of them, for others there don't exist issues, but asking around should yield enough results. You can also
just check, which features you are missing personally. An unordered list of what this could include:

- Set and show canonical and secondary aliases for rooms.
- Edit power_levels.
- Restrict certain actions, if a user does not have the power to do them.
- View user profiles from the member list in a room.
- Manage logged in devices.
- Fix theming issues on different platforms.
- You should be able to autocomplete room names, aliases and `/commands`.
- Read markers are weird.
- Improve scrolling behaviour (on mobile especially).
- Improve behaviour on network loss.
- Improve support for mobile and touch devices (like the PinePhone).

There are probably more issues, that could apply and not all of them have to be fixed as part of GSoC. Pick some you like and include them in your proposal.

#### Contacts

You can reach the mentors for questions via Matrix in the #nheko-reborn:matrix.org room or directly:
- red_sky (@red_sky:ocean.joedonofry.com)
- Nico (@deepbluev7:neko.dev)

#### Milestones

The milestones are just a general timeline, you may want to move some elements to a closer milestone to have more time for fixing bugs in the last few weeks, since time can be an
issue shortly before the deadline.

##### Before GSOC

* Get familiar with Nheko.
* Ask around for issues others would like to have fixed or discover your own bugs or missing features.
* Join #nheko-reborn:matrix.org and get to know the contributors and community.
* Clone the [nheko repo](https://github.com/Nheko-Reborn/nheko/) and compile the current dev branch.
* Maybe you can find something small to contribute to get familiar with the code, development and the contribution process. There is probably a typo or a bad ui layout somewhere in the
    code.

##### GSOC CODING STARTS

* Pick a few issues, that you think you can finish in Phase 1.
* Communicate what you are working on and start implementing and discussing solutions.
* Let your issues be reviewed sequentially, when they are ready. You may start working on the next issue, while the first is in review and so on.
* See that your Pull Requests get merged and the corresponding issues get closed.

##### GSOC FINAL

* Ensure all previous issues have come to a close.
* Pick a few more issues and solve them.
* Only start issues, that you are confident you will be able to complete before the final evaluation!
