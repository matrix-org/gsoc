---
name: New backends for Bifrost
desc: Connect other protocols to Matrix using the new Bifrost bridge!
requirements:
# Student requirements:
 - Keen interest in bridging networks together
difficulty: Medium
issues:
mentors:
# First person in contact; mentors may change before project starts.
 - Half-Shot
initiatives:
 - GSOC
tags:
 - Node.JS
 - Typescript
 - Bridges
---
Bifrost is a new bridge for Matrix, which lets Matrix users chat to people on
other protocols seamlessly. It is designed to work with multiple protocols
and currently supports XMPP, and basic support for a variety of libpurple protocols.

The project uses various "backends" to connect protocols up, which
are abstracted away from the Matrix code. You can hack away support for your favorite
protocol in isolation from the Matrix code, and then simply run it.

#### And this is where you come in

We need more backends to other networks on the bridge, as well as more refinements
to Bifrost itself. Existing bridges can be found on
https://matrix.org/docs/projects/bridges which might be useful. There is also
a [wishlist](https://github.com/turt2live/matrix-wishlist/issues?q=is%3Aopen+is%3Aissue+label%3Abridge)
of protocols that could be added to the bridge.

A familiarity with Node.JS or Javascript will be helpful to you, but this is not
a hard requirement.

#### Expected Results
The output of this project should be a somewhat stable backend
which can be used to talk to another protocol. Any features or bug fixes to
Bifrost's Matrix layers are a bonus!

Please check out https://github.com/matrix-org/matrix-bifrost for information
on the project.
