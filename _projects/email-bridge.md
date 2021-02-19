---
name: First-Class Email Bridge
desc: Build a "gateway" email bridge to Matrix
requirements:
# Student requirements:
 - Keen interest in bridging networks together
difficulty: Hard
issues:
mentors:
# First person in contact; mentors may change before project starts.
 - Half-Shot
initiatives:
 - GSoC
tags:
 - Node.JS
 - Typescript
 - Bridges
 - Email
 - SMTP
---

Email is one of the most ubiquitous methods on the Internet to communicate today, having
been around for a very long time. It's been a dream for a long time that one day Matrix
could be connected up to Email by translating incoming [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol)
traffic to Matrix messages, and then bridging Matrix messages back into emails. 

Matrix has a long history of being the best place to bridge different networks together. It
has a [rich ecosystem of bridges](https://matrix.org/bridges/), making full use of the
[Application Service API](https://matrix.org/docs/spec/application_service/r0.1.2). There
are some Email bridges in existence already but here we are looking for someone to go
above and beyond and build a native SMTP <-> Email bridge.

### And this is where you come in

We'd like you to build a Email bridge to Matrix. This would ideally take the form of a
bridge process that handles its own SMTP traffic rather than using an existing mail
server, and would bridge messages to and from Matrix rooms based upon the room membership
rather than any kind of storage in the bridge. This is typically what we call a gateway
bridge where the user has to do no extra configuration to make rooms magically bridge!

Ideally, a user could send an email to an address like `room+matrix_matrix.org@matrix.org`
and the user would be automatically joined to `#matrix:matrix.org`, and the message
would appear in the room. The user would also be subscribed to the room similar to a
mailing list so they could see responses.

Several base libraries exist such as:
 - [matrix-appservice-bridge](https://github.com/matrix-org/matrix-appservice-bridge/) (Typescript/JavaScript)
 - [matrix-bot-sdk](https://github.com/turt2live/matrix-bot-sdk) (Typescript/JavaScript)
 - [mautrix-go](https://github.com/tulir/mautrix-go) (Go)
 - Or any other library that supports the appservice API 🚀 

### Expected Results

At it's most basic form, the bridge would be able to send messages to a Matrix room
and send messages from a Matrix room to a set of subscribers. There is scope for extra
features like HTML handling, attachments, End-2-End encryption support and more though!

Come hang out and chat to us in [#bridges:matrix.org](https://matrix.to/#/#bridges:matrix.org?via=half-shot.uk&via=matrix.org&via=vector.modular.im)
and take a look at the bridges listed on [matrix.org](https://matrix.org) to see if you'd
like to give this one a shot!
