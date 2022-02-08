---
name: Peer-to-peer Quotient
desc: Embed a homeserver into libQuotient
requirements:
 - Good C++11 (C++17 is a plus)
 - Basic knowledge of Qt (QObject, signals/slots)
 - Understanding of Matrix architecture
 - Backround in p2p systems is a plus
 - Experience in Dendrite configuration is a big plus
difficulty: high
issues:
mentors:
 - KitsuneRal
initiatives:
 - GSoC
tags:
 - Qt
 - Golang
---

#### Description

One of the actively researched areas in Matrix is making it work in peer-to-peer
setting, when a homeserver resides right next to the client and the two are
deployed together. Dendrite has recently reached a good level of feature parity
to participate in the public federation, and has been used for experiments
to embed a homeserver in a web-based Matrix client.

libQuotient is a client-side library based on Qt to interact with Matrix servers.
You're invited to repeat the exercise with embedding Dendrite, this time into
a desktop client. You can use either Quaternion or NeoChat as the client
application to bundle Dendrite with.

#### Milestones

##### GSOC CODING STARTS

* Learn what's been done on the topic of embedding homeservers so far
* Get familiar with libQuotient and the client application code base

##### GSOC MIDTERM

* Show a fixed homeserver configuration deployed and managed together with a client

##### GSOC FINAL

* Complete a distributable package of Dendrite and the client application that
  installs and provides necessary configuration controls to run both as a whole.
