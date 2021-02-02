---
name: Extend Ruma's API coverage
desc: Extend Ruma's coverage of the Matrix APIs and associated MSCs.
requirements:
 - Some prior experience with Rust
difficulty: low
issues:
 - https://github.com/ruma/ruma/milestone/3
 - https://github.com/ruma/ruma/issues/247
 - https://github.com/ruma/ruma/issues/365
mentors:
 - jplatte
initiatives:
 - GSoC
tags:
 - Rust
---

Ruma is a set of Rust library crates for working with the Matrix protocol.
You can learn more about the project on [www.ruma.io](https://www.ruma.io/).

#### Description

Ruma already has crates for all of the APIs that are part of the Matrix
specification, but they don't cover everything that is specified, and much less
many of the MSCs that are implemented in Element, Synapse, and other
Matrix-related software.

To get a feeling for what kinds of specified things are still missing, have a
look at the related issues. In terms of [MSCs], pretty much anything is fair
game, though some more complex MSCs might require additional mentor power to be
feasible for GSoC.

[MSCs]: https://matrix.org/faq/#what's-an-msc%3F
