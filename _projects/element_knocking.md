---
name: Implement Support for Knocking in Element Web
desc: Add support for Matrix's knocking feature in Element Web
requirements:
 - Matrix Client-Server API familiarity
 - Javascript & React
difficulty: high
issues:
 - https://spec.matrix.org/v1.2/client-server-api/#knocking-on-rooms
mentors:
 - TravisR
initiatives:
 - GSoC
tags:
 - Javascript
 - React
---

#### Description

Knocking allows prospective members of a room to ask for an invite directly
instead of having to go through alternative, out of band, means to get an
invite. If their knock is accepted, they can then become a proper member of the
room. 

Element Web/Desktop doesn't currently offer a way to knock on rooms
easily though - the scope of this project would be to fix that, and to expose
knocks to room moderators for review.
