---
name: 3rd Party Authorised Invites
desc: Invite your users to a room based on some external authorisation. 
# add a short one line description of your project
requirements:
 - Understanding of the matrix Client-Server API
difficulty: medium
issues:
mentors:
 - Cadair
initiatives:
 - GSoC
tags:
---

#### Description

This project aims to fill a gap which currently exists in the matrix
ecosystem, which is the ability to delegate membership of a room to a third
party service.

Two examples of this workflow include:

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

* A web based admin panel, where the relationship between rooms and third party
  groups could be configured.
* The ability to use [token-authenticated registration](https://spec.matrix.org/v1.2/client-server-api/#token-authenticated-registration)
  to offer accounts on a specific homeserver to authorised users.

**Related Projects**

 - https://github.com/matrix-org/matrix-user-verification-service

#### Milestones

##### GSOC CODING STARTS

* Be awesome

##### GSOC MIDTERM

* Have done awesome stuff.

##### GSOC FINAL

* Finished the awesome stuff.
