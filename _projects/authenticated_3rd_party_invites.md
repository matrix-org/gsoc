---
name: 3rd Party Authorised Room Membership
desc: Invite and kick users in a room based on a external authorisation source. 
requirements:
 - Understanding of the Matrix Client-Server API
difficulty: medium
issues:
mentors:
 - Cadair
 - Half-Shot
initiatives:
 - GSoC
tags:
 - Javascript & React
 - A programming language with a good matrix SDK (for the server side component)
 - 350h
---

#### Description

This project aims to fill a gap which currently exists in the matrix
ecosystem, which is the ability to delegate membership of a room to a third
party service.

We envisage a workflow where a user authenticates with both matrix and the
third party service, so that the bot can link the two identities and issue
invites. The bot could also keep access to the third party account to monitor
for changes with would lead to revoking room membership.

Three examples of this workflow include:

1. A (Patreon) supporters room: if you support a project at a certain level you
   get access to a supporters room. In this situation, the support platform
   (Patreon) provides an API which when authenticated as a user tells you what
   level of support they are giving. This information could then be used to
   invite a matrix account to a room.
2. A room for all the people who are in a "maintainers" team on GitHub (etc.).
   In this case a person can login to the invite bot with their GitHub account
   and their matrix account and invites will be issued to the relevant rooms.
3. A invite URL. If you have the URL you can login as a matrix user and get an
   invite to the room.

The way we envisage this working is in three core components:

* A server-side component including: matrix bot which can invite users to the
  rooms, the ability to use
  [OpenID](https://spec.matrix.org/v1.2/client-server-api/#openid) to verify
  ownership of a matrix ID, and a plugin for a third party authorisation
  service.
* A Javascript frontend which logs into the matrix account and gets an OpenID
  token to pass to the backend. Using OpenID like this allows the server to
  verify the matrix id of the invitee while not having an access token for the
  users matrix account.
* A plugin system allowing the server admin to configure what third party
  systems to use for authorisation.

Other extensions to this project could include:

* Perodic checks against the third party service to kick people from the rooms
  if they are no longer authorised to be there.
* A web based admin panel, where the relationship between rooms and third party
  groups could be configured (and support for using this as a widget in
  a matrix room).
* The ability to use [token-authenticated registration](https://spec.matrix.org/v1.2/client-server-api/#token-authenticated-registration)
  to offer accounts on a specific homeserver to authorised users.
* The functionality to kick people from more rooms than the bot invites them
  to. This would enable the invite bot to invite users to a space where the
  rooms it contains use 
  [restricted join rules](https://spec.matrix.org/v1.2/client-server-api/#restricted-rooms)
  and let users join as many rooms as they wish.
  The issue with this currently is that if the user is kicked from the space,
  they are still a member of all sub-rooms, so they would need to be explicitly
  kicked from those rooms as well.

**Related Projects**

 - https://github.com/matrix-org/matrix-user-verification-service

**Implementation**

The server side of this project could be implemented in any language, although
the mentors are most familiar with Python, node and rust.

The client side components would best be written in Type/Javascript & React.
A good secondary outcome of this project would be a reusable Matrix login
component written in React.

#### Milestones

##### GSOC CODING STARTS

* Have agreeded an implementation plan with the mentors, including choice of
  programming language.
* Have setup a local development environment and pushed initial project
  configuration to the new repository.

##### GSOC MIDTERM

* Have a working login component with OpenID handoff to the server.
* Have implemented a matrix bot which can invite users.
* Have a working URL > matrix login > recieve invite workflow.

##### GSOC FINAL

* Designed an interface for third party plugins and implemented at least one
  example.
* Implemented kicks if the third party plugin supports it.
* Documented setup and configuration of the project to make it easy for people
  to host instances.
