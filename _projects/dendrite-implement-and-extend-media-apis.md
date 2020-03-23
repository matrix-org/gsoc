---
name: "Dendrite: Implement and extend media APIs"
desc: "This involves implementing media endpoints over federation, as well as extending the APIs to support being backed by AWS S3 and an in-memory store for peer-to-peer in-browser servers."
difficulty: "Hard"
issues:
 - https://github.com/matrix-org/dendrite/issues/775
 - https://github.com/matrix-org/dendrite/issues/629
 - https://github.com/matrix-org/dendrite/issues/621
mentors:
 - Kegsay
 - neilalexander
initiatives:
 - GSoC
tags:
 - Server
 - Dendrite
---

[Dendrite](https://github.com/matrix-org/dendrite) is a work in progress matrix homeserver written in Go. 

This project involves implementing media endpoints over federation, as well as extending the APIs to support being backed by AWS S3 and an in-memory store for peer-to-peer in-browser servers.

* S3 for mediaapi #775
* Media API: Media metadata (hash, size…) aren't stored in db for media fetched remotely #629
* Implement missing media APIs #621
* in-memory gzip for p2p
