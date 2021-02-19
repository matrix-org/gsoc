---
name: Maths support
desc: Add support for sending an displaying messages with mathematical notation.
requirements:
# Student requirements:
 - Python
 - JavaScript
difficulty: easy
issues:
# Related issues (if any)  to this project.
 - https://github.com/vector-im/riot-web/issues/1945
 - https://github.com/matrix-org/matrix-doc/pull/2191
mentors:
# First person in contact; mentors may change before project starts.
 - uhoreg
 - Cadair
initiatives:
 - GSoC
tags:
# Different technologies needed
 - MathJax
 - python
 - javascript
---
#### Description

The ability to send messages with mathematical notation is a frequently
requested feature in Matrix and Riot.  The [riot-web
issue](https://github.com/vector-im/riot-web/issues/1945) is one of the issues
with the most thumbs up reactions in riot-web.  Implementing the ability send
mathematical notation would require ensuring that it is done in a way that is
consistent with the Matrix specification, and ensuring that other receiving
clients display something usable to users, even if they don't have maths
support built-in.

A [Matrix spec change
proposal](https://github.com/matrix-org/matrix-doc/pull/2191) has been made for
adding this capability, and a [partial
implementation](https://github.com/matrix-org/matrix-react-sdk/pull/3251) has
been made.

In this project, you would pick a client, or multiple clients, to implement
maths support in.  There may be a server-side component to the work, as one
possibility is to add an endpoint in the homeserver to render an image of the
mathematical notation, to help clients in generating a fallback representation.

#### Expected Results

Extend one or more Matrix clients to allow users to write messages with
mathematical notation, and to display messages written by others.
