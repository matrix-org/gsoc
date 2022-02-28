---
name: Bridge Discord Servers as Matrix Spaces
desc: Make matrix-appservice-discord Server go beyond single channel bridging
requirements:
 - Knowledge of the Discord API
difficulty: high
issues:
 - https://github.com/Half-Shot/matrix-appservice-discord/issues/738
mentors:
 - reivilibre
 - turt2live
initiatives:
 - GSoC
tags:
 - typescript
 - 175h

---

#### Description

The `matrix-appservice-discord` bridge supports bridging individual Discord
channels to Matrix. When communities relying on Discord want to open up to
Matrix, they need to be able to bridge their whole Discord Server to a Matrix
Space at once.

The base project is to get the bridge to create a new Matrix Space per Discord
Server and one new Matrix room per Discord channel, and bridge them together.

Some extensions to the project can make the bridge more flexible (e.g. by giving
the possibility to add rooms to an existing Space).

#### Milestones

##### GSOC CODING STARTS

* Deploy a local Synapse server
* Deploy `matrix-appservice-discord`
* Bridge a dummy Discord Server using the bridge

##### GSOC MIDTERM

* The bridge is capable of creating a Matrix Space and populating it with Matrix
  rooms corresponding to the Discord channels, even if the rooms are not
  actually bridged.

##### GSOC FINAL

* The bridge is capable of creating a Matrix Space and populating it with Matrix
  rooms corresponding to the Discord channels, and to actually bridge them
  together without requiring a manual intervention of the Discord admin in each
  channel.
* Extension: the bridge is capable of monitoring the Discord Server to add new Matrix rooms to the Space if new channels are created on the Discord Server
