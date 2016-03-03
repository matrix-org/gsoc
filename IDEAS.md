Google Summer Of Code Matrix Ideas list
=======================================

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [Google Summer Of Code Matrix Ideas list](#google-summer-of-code-matrix-ideas-list)

  - [What is Matrix?](#what-is-matrix)
  - [APIs and architecture:](#apis-and-architecture)
  - [Code repositories:](#code-repositories)
  - [Potential GSoC ideas:](#potential-gsoc-ideas)
  - [This is list is now prioritised - most important suggestions first (as of Mar 1st 2016)](#this-is-list-is-now-prioritised---most-important-suggestions-first-as-of-mar-1st-2016)
    - [Bridge ALL THE THINGS!!](#bridge-all-the-things)
    - [Integrations to ALL THE THINGS!!](#integrations-to-all-the-things)
    - [Internationalising Matrix](#internationalising-matrix)
    - [Matrix Visualisations](#matrix-visualisations)
    - [HTML Embeddable Matrix Chat Rooms](#html-embeddable-matrix-chat-rooms)
    - [IPFS support for content repositories](#ipfs-support-for-content-repositories)
    - [Alternative Efficient Client-Server Transports and Encodings](#alternative-efficient-client-server-transports-and-encodings)
    - [Helping out on PTO](#helping-out-on-pto)
    - [Extending Native Matrix Desktop Clients](#extending-native-matrix-desktop-clients)
    - [Helping out on Ruma (Rust Homeserver)](#helping-out-on-ruma-rust-homeserver)
    - [Matrix Powered Microblogging](#matrix-powered-microblogging)
    - [Editable messages](#editable-messages)
    - [Location based Chat](#location-based-chat)
    - [Decentralised reputation](#decentralised-reputation)
    - [Decentralised Search](#decentralised-search)
    - [Synapse optimisation](#synapse-optimisation)
    - [IPv6 Support](#ipv6-support)
    - [IoT Dashboard with Matrix](#iot-dashboard-with-matrix)
- [Ideas below this point almost certainly require more effort than the GSoC format allows, but are included here for interest's sake.](#ideas-below-this-point-almost-certainly-require-more-effort-than-the-gsoc-format-allows-but-are-included-here-for-interests-sake)
    - [E2E Encryption](#e2e-encryption)
    - [Peer-to-peer Matrix](#peer-to-peer-matrix)
    - [Decentralised accounts](#decentralised-accounts)
    - [Decentralised identity](#decentralised-identity)
    - [Etherpad clone](#etherpad-clone)
    - [Collaborative Whiteboarding in Matrix](#collaborative-whiteboarding-in-matrix)
    - [Music jamming over Matrix](#music-jamming-over-matrix)
    - [Matrixcraft](#matrixcraft)
    - [Threaded Matrix client](#threaded-matrix-client)
    - [Matrix Virtual World](#matrix-virtual-world)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

What is Matrix?
---------------

Matrix is a decentralised communication specification for clients and servers.  It is designed to replicate conversation data across multiple servers via federation, meaning that there are no single points of control or failure for conversations or their history.  Anyone can run their own "home" server, or use one hosted by someone else (e.g. ``matrix.org``). All communication uses HTTP(S) and data is represented as JSON objects, scoped to a "room", which consists of a group of users.  Matrix is designed to make it easy to bridge existing communication apps and networks, making Matrix a global decentralised "meta-network" for connecting (or matrixing!) together all of today's communication silos.

Matrix is completely open and transparent: all of our designs, implementations, testing and bug tracking are publicly available on Github and matrix.org, and our day-to-day design discussions take place on public channels on ``matrix.org``. Anyone can contribute to the specification to help improve it. We also provide reference implementations of a [python server](https://github.com/matrix-org/synapse) and clients in [React](https://github.com/vector-im/vector-web), [Android](https://github.com/matrix-org/matrix-android-sdk) and [iOS](https://github.com/matrix-org/matrix-ios-sdk).

To date, Matrix has been used as a communications protocol for a wide range of technologies, including (but not limited to):
- [Instant messaging](https://vector.im)
- [WebRTC](http://www.webrtcworld.com/videos.aspx?vid=10786)
- [Internet of Things](https://fosdem.org/2015/schedule/event/deviot04/)
- Program-specific data (MIDI, 3D animations)

In the end, we hope Matrix will crack the problem of a widely successful open federated platform for communication on the internet, which bridges together all of today's existing communication silos into a single open communication meta-network.


APIs and architecture:
----------------------
In Matrix, a user account belongs to a homeserver and looks like this: *@localpart:domain* - the localpart is the "username" and the domain is the homeserver on which the account belongs. In other words, *@user1:matrix.org* is a different user to *@user1:example.com* as they are registered on different homeservers. 

In the Matrix network, anyone can run a homeserver. Anyone can also run a client, and you can connect to any homeserver from any client.

A client typically represents a human using a web application or mobile app. Clients use the ["Client-to-Server" (C-S) API](http://matrix.org/docs/spec/r0.0.1/client_server.html) to communicate with their homeserver, which stores their profile data and their record of the conversations in which they participate.

A "homeserver" is a server where conversation history and user accounts are stored, and provides C-S APIs and has the ability to federate with other HSes to replicate conversation history across all the servers which participate in a given room via the [Federation API](http://matrix.org/docs/spec/r0.0.1/server_server.html). It is typically responsible for multiple clients. "Federation" is the term used to describe the sharing of data between two or more homeservers.

Finally, "application services" are privileged clients which can provide bridges and integrations to other networks and platforms, exposing 'virtual' users and rooms which map through to concepts outside of Matrix.  These are fundamental to bridging existing silos into Matrix, and are specified in the ["Application Service API"](http://matrix.org/docs/spec/r0.0.1/application_service.html).

Here is a diagram of this architecture:

                       How data flows between clients
                       ==============================
     
     { Matrix client A }                  { Matrix client B }
         ^          |                         ^          |                   
         |  events  |                         |  events  |                   
         | C-S API  V                         | C-S API  V                   
     +------------------+                 +------------------+                 +-------------+
     |                  |----( HTTPS )--->|                  |----( HTTPS )--->| Application |
     |   Home Server    |                 |   Home Server    |                 |   Service   |
     |                  |<---( HTTPS )----|                  |<---( HTTPS )----|             |
     +------------------+   Federation    +------------------+   App Svc API   +-------------+
                                                                                    |   ^
                                                                                    v   |
                                                                            IRC, Slack, Skype etc

Code repositories:
------------------
Everything is stored under [https://github.com/matrix-org](https://github.com/matrix-org/):
* [Reference python server](https://github.com/matrix-org/synapse)
* ['Vector' React client and SDK](https://github.com/vector-im/vector-web)
* [Reference Android client and SDK](https://github.com/matrix-org/matrix-android-sdk)
* [Reference iOS client and SDK](https://github.com/matrix-org/matrix-ios-sdk)
* [JavaScript client SDK](https://github.com/matrix-org/matrix-js-sdk)
* [Python client SDK](https://github.com/matrix-org/matrix-python-sdk)

...and many many more: see https://matrix.org/blog/try-matrix-now for the full list of existing projects.


Potential GSoC ideas:
---------------------
Remember that you can also use these as inspiration and suggest your own project ideas.

## This is list is now prioritised - most important suggestions first (as of Mar 1st 2016)

### Bridge ALL THE THINGS!!

The single biggest thing missing from the Matrix ecosystem right now are mature bridges to link into other silos and defragment them.
Right now we have beta-grade bridges for IRC, Slack and FreeSWITCH, and alpha-grade bridges for libpurple (Skype, Lync, Telegram, Facebook, WhatsApp etc), Asterisk and Kamailio.

Bridges are relatively easy and fun to write, and we would *love* for GSOCers to get involved in writing new bridges and polishing the existing ones.  Improving the libpurple bridge would be a major win, but so would writing new native bridges.

An example guide for how to write a Slack bridge in 100 lines(!) of Node.js is at https://github.com/matrix-org/matrix-appservice-bridge/blob/master/HOWTO.md - and other existing bridges live at:

 * https://github.com/matrix-org/matrix-appservice-irc
 * https://github.com/matrix-org/matrix-appservice-slack
 * https://github.com/matrix-org/matrix-appservice-verto
 * https://github.com/matrix-org/matrix-appservice-respoke
 * https://github.com/matrix-org/node-purple/tree/master/appservice
 * ...and the full list at https://matrix.org/blog/try-matrix-now under Application Services.

By default our preferred language for writing bridges is in Node.js (ES6), so we can build on top of the https://github.com/matrix-org/matrix-appservice-bridge library which provides a bunch of useful infrastructure and boilerplate.  If the remote network lacks good Node library support we consider other languages though.

In an ideal world, we'd end up with bridges to all of the below and more!

 * Chat systems
  * IRC
  * Slack
  * libpurple
    * Skype
    * Lync
    * FB Messenger
    * Telegram
    * AIM
    * ICQ
    * Y!
    * QQ
    * Sametime?
  * Hangouts
  * WhatsApp
  * HipChat
  * Rocket.Chat
  * Zulip
  * Discord
  * PSYC
  * XMPP
  * MSRP
  * LINE
  * TextSecure / Signal
  * Mattermost
  * iMessage
  * Yammer
  * Cisco Spark
  * Unify Circuit
  * Grape
 * VoIP systems
  * FaceTime
  * PSTN
 * Email systems
  * IMAP
  * SMTP
 * Messageboard systems 
  * NNTP
  * VBulletin
  * phpBB
  * Simple Machines Forum
  * Discourse
 * Blog systems
  * Medium
  * Tumblr
  * Wordpress
  * RSS
  * Twitter
  * Known
 * Social networks
  * Facebook (timeline?)
  * G+ Discussions
  * Buddycloud
  * pump.io
 * Project management feeds
  * Github issues?
  * Github PRs?
  * Trello

**Expected results**: Bridging matrix rooms and users into one or more of the above environments - ideally supporting dynamic users (i.e. auto-creating users on both sides of the bridge on demand) and dynamic rooms (i.e. bridging the whole namespace of the remote network into matrix).

**Difficulty**: Ranges from Easy through to Hard depending on the network!

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Integrations to ALL THE THINGS!!

As well as bridging, we're building out a large ecosystem of integrations (also known as bots) to let folks interact with other services from Matrix.  Today we have basic bots for interfacing with JIRA, Github and Jenkins (https://github.com/matrix-org/Matrix-NEB) and Hubot (https://github.com/davidar/hubot-matrix/) - and we obviously support remote IRC/Slack/XMPP-etc bots via bridging.

Bots can be written in any language, and we have a wide range of SDKs already available to help people get up and running - from everything from Node to Python to Perl to Ruby to Elixir...

Platforms we'd love to integrate with via native Matrix bots include:
 * Trello bot
 * Twitter bot
 * Known bot
 * Giphy
 * Basecamp bot
 * IFTTT
 * Zapier
 * Nagios
 * Google Image search
 * Medium Bot
 * Wordpress Bot
 * HackerNews Bot
 * Reddit Bot
 * Tumblr Bot
 * NNTP Bot
 * VBulletin bot
 * phpBB bot
 * SMF bot
 * Discourse bot
 * ...

Extensions include:
 * Extending bots to be metadata aware: https://github.com/matrix-org/matrix-doc/pull/93 once landed
 * Implementing slack-compatible webhooks

**Expected results**: Creating client-server API bots that respond to !-commands to interact with the given integrated services, and/or inject messages into rooms based on those services.

**Difficulty**: Ranges from Easy through to Medium depending on the service!

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Internationalising Matrix

None of the Matrix clients are currently internationalised.  This is a real shame, especially given that the core dev team is made up of many different nationalities (English, French, Norwegian, etc).  This would be an easy but very useful project to go through implementing consistent internationalisation support across all of our reference clients and servers, working with the wider Matrix open source community to source translations as required.

**Expected results**: Architectural support for i18n in all reference matrix clients and servers, and implementations of at least 4 languages (translation provided by the wider community).

**Difficulty**: Easy / Moderate

**Knowledge pre-req**: Basic Javascript, iOS, Android.

**Potential mentor**: David Baker ([github](https://github.com/dbkr))


### Matrix Visualisations

When developing on Matrix it's often quite hard to visualise the underlying replicated Directed Acyclic Graph datastructure that describes the conversation history in a room.  We've made some basic tools in the past like https://github.com/Kegsay/matrix-vis and https://github.com/matrix-org/synapse/tree/master/contrib/graph but what would be really cool would be a real-time visualisation of the DAG to help folks understand Matrix, and help developers debug interesting edge cases and merge resolution scenarios when the DAG bifurcates.  This could be written in any language, talking some combination of the server-server API or an enhanced version of the client-server API or just inspecting your synapse's database to visualise what's going on.

**Expected results**: A realtime visualisation of the DAG of a given Matrix room, as seen from the perspective of one or more HSes.

**Difficulty**: Medium

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Erik Johnston ([github](https://github.com/ErikJohnston)) or Kegan Dougal ([github](https://github.com/Kegsay))


### HTML Embeddable Matrix Chat Rooms

Blogs and articles that allow users to engage with the author and comment on the content are standard in today's web and hugely popular. The implementations of these are largely from the authors of the blog or often completely proprietary in the case of newspaper or magzine articles. If I comment on a article and start discussing it with someone else, I now have to keep going back to that article to continue the discussion.

Matrix could be used as a platform where users can arrive at a random website, sign in with their Matrix ID, comment on a blog post or article and then continue that discussion through a standard Matrix client.

**Expected Results**: Extending https://github.com/matrix-org/matrix-react-sdk to provide reusable web compoents that a website author can download, embed and skin into their website to make comments work with minimal work to integrate. Could require user to log in with a matrix account to post (so your Matrix account would let you post comments on any website which used this), or support anonymous guest access. The blog author would be able to add their own comments and moderate comments. VoIP and Video calling support would be an added bonus. Other extensions would be plugins for blogging platforms so users of WordPress or similar can use the software on their blogs by just installing the plugin.

**Difficulty**: Easy/Moderate

**Knowledge pre-req**: HTML, Javascript

**Potential mentor**: David Baker ([github](https://github.com/dbkr)), Erik Johnston ([github](https://github.com/erikjohnston)), Kegan Dougal ([github](https://github.com/Kegsay))


### IPFS support for content repositories

Currently Matrix uses a basic distributed content repository based on replicating data over HTTPS between its servers.  It could be nice to support storing data in IPFS instead, providing dedicated p2p distributed immutable data storage rather than the stop-gap solution that Matrix provides.

**Expected Results**: Extend synapse to optionally store and load content from IPFS, and extend one or more matrix clients (e.g. Vector) to natively load/store content from IPFS clientside.

**Difficulty**: Medium

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))


### Alternative Efficient Client-Server Transports and Encodings

Matrix's baseline Client-Server API is simple long-polling HTTP calls.  This is purely for compatibility and simplicity for the widest range of client devices and applications, however - we encourage and expect people to implement more efficient transports and encodings in future.  For instance, we've published and implemented a beta Websockets transport draft at https://github.com/matrix-org/matrix-doc/blob/master/drafts/websockets.rst and https://github.com/matrix-org/matrix-websockets-proxy.

It would be *really* fun to experiment with other transports and encodings to find just how fast, low latency, low CPU or low bandwidth one can make the Client Server API run.  This could involve playing around with COaP+CBOR, MQTT, protobufs, capnproto, messagepack, HTTP/2 or any other option in a quest for the holy grail transport/encoding combination!

**Difficulty**: Medium

**Knowledge pre-req**: Network protocols

**Potential mentor**: Richard van der Hoff ([github](https://github.com/richvdh))


### Helping out on PTO

https://pto.im (Perpetually Talking Online) is an awesome new contribution to Matrix that provides an IRC front-end to any Matrix homeserver, written in Rust, which means anyone can point their existing IRC clients into Matrix, treating as a giant distributed ircd.  This helps people get up and running in the Matrix ecosystem without having to jump all the way to a Matrix client (or bridge via an existing IRC network).  It's very alpha currently, but fun to hack on and there's a wide range of issues to be picked from at https://github.com/tdfischer/pto/issues.


### Extending Native Matrix Desktop Clients

There are several native Matrix Desktop Clients out there:

 * Tensor (QML + JS)
 * Quaternion (QML + C++)
 * Unplug (JavaFX)

 All of which could be extended further.  Developers wanting to hack features into fun desktop clients would be welcome here!

**Expected results**: Add new features to Tensor, Quaternion, Unplug and friends.

**Difficulty**: Easy to Moderate

**Knowledge pre-req**: Familiarity with web services, the language used for implementing the client (e.g. ObjectiveC, Java)

**Potential mentor**: Erik Johnston ([github](https://github.com/erikjohnston)), David Baker ([github](https://github.com/dbkr))



### Helping out on Ruma (Rust Homeserver)

Ruma (https://ruma.io) is a new project from the community to implement a Matrix homeserver in Rust.  It's early days, but it would be great to have both client-side and server-side components for Matrix implemented in Rust, and there's a huge amount of work to be done there.

**Expected Results**: Extend Ruma's components to implement more Matrix endpoints.

**Difficulty**: Hard

**Knowledge pre-req**: Rust, Web Services

**Potential mentor**: Erik Johnston ([github](https://github.com/erikjohnston))


### Matrix Powered Microblogging

Matrix-powered, open and federated microblogging platform. Basically, implement something like [Twitter](http://twitter.com) in Matrix - users can post updates and follow each other, and subscribers get a feed of the users they follow. The great thing with using Matrix for something like this, is that other clients can view and respond to updates from the microblogging application - as long as the common Matrix message types are used.

**Expected results**: User can log in, choose some users to follow, get an aggregated feed of 'tweets' from users they follow, and post 'tweets'.  Messages should be sendable and consumable by both generic Matrix clients as well as the microblog-specific optimised user experience. A web client would probably be the standard with mobile clients as extensions.

**Difficulty**: Moderate

**Knowledge pre-req**: HTML, CSS, Javascript

**Potential mentor**: David Baker ([github](https://github.com/dbkr))


### Editable messages

A relatively easy extension to the Matrix spec and implementation is to add 'update' type messages, letting you edit existing messages, and associate new events with existing ones.  This would provide the long-awaited ability to edit messages.

**Expected results**: Define and implement 'update' message semantics in conjunction with the team.

**Difficulty**: Moderate

**Knowledge pre-req**: Python, and familiarity with at least one of the languages of the current clients (React, Android or Objective C)

**Potential mentor**: Erik Johnston ([github](https://github.com/erikjohnston))


### Location based Chat

A mobile app that shows you a list of chat rooms "around you". People could create chat rooms fixed in one place (a Café could have a room, for example) or you could create a chat room that follows you around as you walk around using the app. Perhaps users could also see other users around them and create chats with them if they had the app open, or see what other chats they were in.

Some level of moderation would likely be necessary - this could be a natural extension once the base features have been implemented. 

A lot of code for the chat itself can be implemented with reusable UI components of the Matrix Console apps. It should be relatively straightforward to allow users to post pictures, video and audio clips to the room using standard Matrix message types and reusable components. 

**Expected Results**: An app and backend where you can log in, create a room, find and join rooms near you and chat.

**Difficulty**: Moderate

**Knowledge pre-req**: Android/iOS, probably python and SQL for the backend.

**Potential mentor**: David Baker (iOS)  ([github](https://github.com/dbkr)), Kegan Dougal (Android) ([github](https://github.com/Kegsay))


### Decentralised reputation

Mitigating abuse is an ongoing area of research in Matrix.  Tracking realtime reputation data for Matrix endpoints, such that users can report abuse and filter their communication to hide abusive content is the holy grail.  There are some very early thoughts on this [here](https://github.com/matrix-org/matrix-doc/blob/master/drafts/reputation_thoughts.rst).  Anyone interested in researching the holy grail of abuse mitigation is welcome to experiment here!

**Expected Results**: Add upvote/downvote functionality to Matrix spec, gather the data in a secure decentralised datastructure that can be mined for cluster analysis, and publish reputation data that Matrix clients can align themselves with when filtering abusive content.

**Difficulty**: Hard

**Knowledge pre-req**: Distributed data-structures; Graph databases; Data analytics

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))


### Decentralised Search

Matrix provides a basic full-text search API and implementation in Synapse.  Would be great to build a cross-Matrix search engine however, especially a decentralised one.

**Expected results**: A Matrix spider that consumes public event data from Matrix and indexes into a decentralised secure datastructure that can then be queried for rapid cross-Matrix search results.

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Familiarity with web services, the language used for implementing the application service (e.g. Python if using our reference example service framework).  Basic HTML/CSS/Javascript needed to implement the search engine interface frontend.

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Synapse optimisation

Synapse is Matrix's reference homeserver, written in Python 2 and Twisted.  It was never written for speed, and there is huge room for optimisation on it.  In the longer term we plan to move to an entirely different codebase, but in practice the Synapse codebase is here to stay and there are lots of people running it who would love to see it faster.  A possible angle here could be to try porting it to PyPy to see if that speeds everything up - as well as a large range of caching and algorithmic profiling and improvement.  Any work here would probably necessitate building better profiling tools for Twisted.


### IPv6 Support

Synapse doesn't currently support IPv6, thanks to limitations on Twisted.  Whilst in the long term we plan to migrate away from Twisted, meanwhile Twisted's IPv6 support is slowly evolving: e.g. recent activity on https://twistedmatrix.com/trac/ticket/4362.  Working with the Twisted team to finish IPv6 and bring it to Synapse would be much appreciated by all the folks running Synapse out there - especially for use on IPv6 overlay networks like cjdns.


### IoT Dashboard with Matrix

Matrix is ideal as a platform for the Internet of Things: simple, federated, persistent communication would allow devices and hubs to communicate with services and one another in a unified, open and extensible way. IoT devices and hubs could send their data into Matrix which would distibute and store it as necessary. 

This project would involve input into a set of standards for such devices to put data into Matrix as well as client of some kind for visualising, analysing and orchestrating the data from these devices and potentially interacting with them. This could take the form of a webapp which reads the data from Matrix (using the React SDK) and/or similar mobile clients. The client would display a list of all of my devices that were feeding data into the system and a summary of the data they're sending, allowing me to view a summary of recent data or get more detail and potentially plot graphs of the data from devices (for example, the current temperature of my home thermostat and its trend over the last month). 

It's important that the system is open and usable by others, so specifying a format for data that's as flexible as possible whilst also providing rich, detailed information from each type of device would be an interesting problem.

**Expected results**: one IoT dashboard web application, with some IoT devices integrated via the Matrix client-server API.  Optionally also IoT application services for analysing/aggregating/visualising the resulting IoT data en mass.

**Difficulty**: Moderate

**Knowledge pre-req**: Javascript/HTML5/React/CSS for web application.  Python or similar for IoT application services if using our reference application service framework.

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))


# Ideas below this point almost certainly require more effort than the GSoC format allows, but are included here for interest's sake.


### E2E Encryption

Matrix aims to provide E2E encryption as part of the baseline spec.  The job is currently half done - we have an excellent Axolotl-style cryptographic ratchet called [Olm](https://matrix.org/git/olm), but have yet to wire it into Matrix itself - see https://matrix.org/jira/browse/SPEC-162 for the gory details of the work that remains.  Integrating Olm into both the matrix spec and homeserver implementation (key management etc) and as many clients as possible would be a challenging but incredibly rewarding project for anyone specialising in cryptography.

**Expected Results**: Add Olm-based E2E encryption to Matrix (reference server, spec and reference clients)

**Difficulty**: Hard

**Knowledge pre-req**: Cryptography, C++, JavaScript

**Potential mentor**: Mark Haines ([github](https://github.com/NegativeMjark)), Richard van der Hoff ([github](https://github.com/richvdh))


### Peer-to-peer Matrix

Matrix currently follows a client-server architecture, where the servers federate together.  This means that to host your own conversations in Matrix you have to own and maintain a server with a static IP and DNS SRV record etc.  This isolates many people from running their own Matrix nodes.  An interesting experiment would be to write a homeserver variant (probably in Node.js) which advertises itself via a DHT or similar (e.g. using js-libp2p) and uses WebRTC data channels for p2p synchronisation of message graph data.  This could make it much easier to run homeservers - either as a standalone node daemon, or built into a desktop or even web client.  Such a server would implement the basic features of today's Matrix C-S API, but obviously break compatibility with today's Matrix S-S API.  An extension might be to write a bridge between the two federation protocols.

**Expected Results**: A proof-of-concept P2P Matrix homeserver in Node

**Difficulty**: Hard

**Knowledge pre-req**: P2P tech, JavaScript

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))


### Decentralised accounts

Currently Matrix accounts are stored on a single homeserver.  This is far from decentralised and produces an unfortunate single point of failure and control for the user.  It would be fantastic to evolve Matrix to support replicating account data across multiple servers, and let clients pick which home server they talk to.  There is significant overlap in solving this with the 'Peer-to-peer Matrix' proposal.

**Expected Results**: Extend the matrix spec and homeserver to support decoupling accounts from DNS, and allowing multiple trusted servers to host the data. 

**Difficulty**: Hard

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n)), Erik Johnston ([github](https://github.com/erikjohnston))


### Decentralised identity

Currently the mapping of 3rd party IDs (e.g. email addresses) through to Matrix IDs is performed by a logically centralised ID server.  This project would create a decentralised datastore of ID mappings - e.g. using DataEntry objects in a stellar-core ledger, or some other distributed secure data structure, with trusted identity providers entering verified ID mappings into the store.

**Expected Results**: Replace the current `sydent` ID server implementation with a decentralised equivalent.

**Difficulty**: Hard

**Knowledge pre-req**: Secure distributed data-structures, Security, Cryptography

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n)), Erik Johnston ([github](https://github.com/erikjohnston))


### Etherpad clone

[Etherpad](http://etherpad.org/) is a multi-user, real-time text collaboration tool which we use frequently internally. The aim of this project is to recreate Etherpad using Matrix. As a start, aim for a multi-user "notepad"-style application, and then more advanced features (chat, per-user history, different fonts/text-effects/etc) can be added as extensions.

**Expected results**: Able to have at least 10 people collaborating (typing) on a single document, and to have the document in sync across all people.

**Difficulty**: Hard. Made harder by needing to storing and synchronising document snapshots efficiently.

**Knowledge pre-req**: Python/Twisted for server-side extensions; Client-side development (Javascript/HTML/CSS or Android or iOS), HTTP/JSON APIs, basic awareness of Operational Transform theory.

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Collaborative Whiteboarding in Matrix

Matrix allows clients to send and synchronize arbitary pieces of data in a room, allowing the possibility collabrative editing. This project would be to use this ability to design and implement a collaborative whiteboarding app using Matrix. This is similar to the etherpad project above, except synchronizing a whiteboard canvas between clients instead of text.

**Expected results**: A client that supports allowing multiple users drawing and editing the whiteboard similutaneously, with the results synchronized in real time between all clients in the room.

**Difficulty**: Hard

**Knowledge pre-req**: Python/Twisted for server-side extensions; Client-side development (Javascript/HTML/CSS or Android or iOS), HTTP/JSON APIs, basic awareness of Operational Transform theory

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Music jamming over Matrix

The Matrix team built a "MIDI over Matrix" proof of concept called RemoteJam for TechCrunch Disrupt London 2014 - this was a simple Network MIDI to Matrix bridge which persisted network MIDI traffic into Matrix, and then transcribed it using javascript to musical notation.  This project would extend or reimplement this hack to build a full remote musical jamming solution for Matrix, with no single points of failure or ownership over the resulting music.  Users anywhere on the net would be able to play together via MIDI, storing the data into Matrix for posterity and letting the public listen and view the transcription in realtime.

**Expected results**: one remote jamming web application powered by Matrix, and a MIDI<->Matrix bridge.

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Some knowledge of MIDI and music useful.  Javascript/HTML5/React/CSS for the web application.  Python or similar for the basis MIDI<->Matrix application service bridge.  Knowledge of statistics useful for understanding quantising algorithms for transcribing MIDI.

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))


### Matrixcraft

There are many minecraft clones available e.g. https://github.com/fogleman/Minecraft - but none of these are networked in any way. The aim of this project is to design and implement a protocol which can allow multiple minecraft players to play together, even though they are using different clients - by having the data communication go through Matrix.

**Expected results**: Able to have 2+ players building structures together

**Difficulty**: Hard. Getting sensible chunking algorithms for rooms is Hard. There is huge scope to build on this both feature wise (e.g. PvP, monster AI) and protocol wise (reliability, masking latency hiccups, etc)

**Knowledge pre-req**: Python (assuming fogleman/Minecraft is used as a base)

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Threaded Matrix client

One of the major early uses of Matrix are public rooms (similar to IRC) focused around given topics, for example Matrix support channel, android development, etc. These run into the classic problem of having multiple concurrent conversations in them, which often leads to confusion for all participants. One of the desired features of Matrix is to provide threading support such that individual messages can be marked as a reply to others, this would allow apps to differentiate the various different conversations in the UI giving a much better and more usable user experience.

This project would involve helping to finalize how Matrix supports threading, as well as implementing support in one or more of the current clients.

**Expected results**: A client with support for replying to particular messages and showing the ongoing and historic threads.

**Difficulty**: Moderate

**Knowledge pre-req**: Familiarity with at least one of the languages of the current clients (React, Android or Objective C)

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Matrix Virtual World

This is an extension of both the etherpad, Matrixcraft and Collaborative whiteboarding ideas mentioned above.  By integrating WebGL (e.g. using a library like ThreeJS) with Matrix, one can create a collaborative virtual world whose data is persisted in Matrix, replicated over all participating Matrix homeservers with no single points of control or failure.  If implemented as a generic platform, one could first start off by sharing 3D geometry in the world, and then defining higher level semantics (perhaps in combination with matrix Application Services) to define business logic for the world.  A good example could be building a collaborative 3D model editor on top of Matrix, or a 2D collaborative graphical programming environment.

**Expected results**: A WebGL Matrix client that renders 3D geometry described in Matrix, allowing direct manipulation and operational transforms for concurrent access.

**Difficulty**: Hard

**Knowledge pre-req**: 3D graphics, WebGL, Operational Transform theory all a plus.  Would likely require optimisations and/or extensions to the server to support storing object graphs in Matrix.

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))

