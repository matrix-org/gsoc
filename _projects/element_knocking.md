---
name: Implement Support for Knocking in Element Web
desc: Add support for Matrix's knocking feature in Element Web
requirements:
 - Matrix Client-Server API familiarity
 - Javascript & React
difficulty: high
issues:
 - https://github.com/vector-im/element-web/issues/18655
mentors:
 - kerryarchibald
initiatives:
 - GSoC
tags:
 - Javascript
 - React
 - 175h
---

#### Description

[Knocking](https://spec.matrix.org/v1.2/client-server-api/#knocking-on-rooms)
is a feature added in version 1.1 of the Matrix specification which allows
prospective members of a room to ask for an invite directly instead of having
to go through alternative, out of band, means to get an invite. If their knock
is accepted, they can join the room. 

Element Web/Desktop doesn't currently offer a way to knock on rooms
easily though - the scope of this project would be to fix that, and to expose
knocks to room moderators for review.

#### Milestones

##### GSOC CODING STARTS

* Have setup a local Element web development environment and made a small Pull
  Request to Element Web.

##### GSOC MIDTERM

* Ability to send knocks from room directory and peeks, and alter room settings
to allow people to knock.
* Ability to respond to knocks as a room moderator 

##### GSOC FINAL

* Ability to see your pending knocks somewhere
