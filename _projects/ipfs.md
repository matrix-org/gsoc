---
name: "IPFS support for content repositories"
desc: "Implement a Matrix compatible IPFS media repository."
difficulty: "medium"
issues:
 - https://github.com/matrix-org/matrix-doc/issues/539
mentors:
 - ara4n
initiatives:
 - GSoC
tags:
 - Media
 - ipfs
---

Currently Matrix uses a basic distributed content repository based on
replicating data over HTTPS between its servers. It could be nice to support
storing data in IPFS instead, providing dedicated p2p distributed immutable data
storage rather than the stop-gap solution that Matrix provides.

#### Expected Results

Extend synapse to optionally store and load content from IPFS, and extend one or
more matrix clients (e.g. Riot) to natively load/store content from IPFS
clientside.