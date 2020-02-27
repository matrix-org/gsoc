---
name: Improve code generation in the ruma project
desc: The ruma (Rust & matrix) project would welcome some new codegen macros and improvements to existing ones.
requirements:
 - Rust
difficulty: medium
issues:
 - https://github.com/ruma/ruma-events/issues/47
 - https://github.com/ruma/ruma-api/issues/37
 - https://github.com/ruma/ruma-api/issues/32
 - https://github.com/ruma/ruma-api/issues/35
mentors:
 - jplatte
initiatives:
 - GSoC
tags:
 - Rust
 - Libraries
---
#### Description

Ruma is a Matrix homeserver, client, and supporting libraries written in Rust.
This project is about the libraries part, in particular

* [ruma-events][], which provides a Rust API for working with matrix events
* [ruma-api][], which is a building block for other ruma crates that provide
  Rust bindings to the various matrix APIs (currently there is ruma-client-api
  for the Client-Server API and ruma-appservice-api for the Application Service
  API)

[ruma-events]: https://github.com/ruma/ruma-events
[ruma-api]: https://github.com/ruma/ruma-api

Both of these already employ a decent amount of code generation based on
procedural macros to reduce the amount of code required for event and API
endpoint definitions respectively.

There are some long-standing issues regarding the readability of parts of the
procedural macro code and in ruma-events in particular, there's currently some
boilerplate-heavy code that would again have to be mostly copy-pasted for a
planned feature. A student deciding to work on ruma's code generation could thus
choose whether to start with a clean slate or try to improve some existing code
first.

Since Rust has a relatively high learning curve, prior Rust knowledge is
assumed, but experience with procedural macros or the relevant codegen crates
(syn & quote) is not.

#### Milestones

##### GSoC coding start

After the first days of GSoC,

* you have decided what you want to work on first
* you know where you can ask for help
* you know where to find documentation for the libraries you're working with

##### GSoC midterm

* you're comfortable working on procedural macros
* you have opened a few PRs on ruma-api and / or ruma-events

##### GSoC final

* ruma's procedural macro code is looking better than ever thanks to you!

#### Expected results

* you replaced ruma-events' boilerplate-heavy event collection code with an
  invocation of a new procedural macro
* one or more Pull Requests to ruma-api and / or ruma-events that improved the
  readability of the procedural macro code were opened by you and accepted by a
  maintainer
