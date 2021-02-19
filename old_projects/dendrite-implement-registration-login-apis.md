---
name: "Dendrite: Implement registration/login APIs"
desc: "This involves implementing missing registration features, adding support for Application Services, shared secrets and Single Sign-On. This can be complemented by implementing the OpenID module."
difficulty: "Hard"
issues:
 - https://github.com/matrix-org/dendrite/issues/708
 - https://github.com/matrix-org/dendrite/issues/644
 - https://github.com/matrix-org/dendrite/issues/630
 - https://github.com/matrix-org/dendrite/issues/599
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

This project involves implementing missing registration features, adding support for Application Services, shared secrets and Single Sign-On. This can be complemented by implementing the OpenID module.

* Dendrite needs to care about login flow ordering #708
* Implement missing registration features #644
* Special case /register for application services #630
* Implement OpenID module #599
* impl rest of register/login APIs, SSO, etc
