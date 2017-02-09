Google Summer Of Code Matrix Ideas list
=======================================

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


  - [What is Matrix?](#what-is-matrix)
  - [APIs and architecture:](#apis-and-architecture)
  - [Code repositories:](#code-repositories)
  - [Potential GSoC ideas:](#potential-gsoc-ideas)
  - [This is list is now prioritised - most important suggestions first (as of Feb 9th 2017)](#this-is-list-is-now-prioritised---most-important-suggestions-first-as-of-feb-9th-2017)
    - [Building Bridges!](#building-bridges)
    - [Integrations to ALL THE THINGS!!](#integrations-to-all-the-things)
    - [Internationalising Matrix](#internationalising-matrix)
    - [Matrix Visualisations](#matrix-visualisations)
    - [HTML Embeddable Matrix Chat Rooms](#html-embeddable-matrix-chat-rooms)
    - [IPFS support for content repositories](#ipfs-support-for-content-repositories)
    - [Alternative Efficient Client-Server Transports and Encodings](#alternative-efficient-client-server-transports-and-encodings)
    - [Finishing matrix-ircd](#finishing-matrix-ircd)
    - [Extending Native Matrix Desktop Clients](#extending-native-matrix-desktop-clients)
    - [Helping out on Ruma (Rust Homeserver)](#helping-out-on-ruma-rust-homeserver)
- [Ideas below this point almost certainly require more effort than the GSoC format allows, but are included here for interest's sake.](#ideas-below-this-point-almost-certainly-require-more-effort-than-the-gsoc-format-allows-but-are-included-here-for-interests-sake)
    - [Peer-to-peer Matrix](#peer-to-peer-matrix)
    - [Decentralised accounts](#decentralised-accounts)
    - [Decentralised identity](#decentralised-identity)
    - [Decentralised reputation](#decentralised-reputation)
    - [Decentralised Search](#decentralised-search)
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
* ['Riot' React client](https://github.com/vector-im/riot-web)
* [Reference react SDK](https://github.com/matrix-org/matrix-react-sdk)
* [JavaScript client SDK](https://github.com/matrix-org/matrix-js-sdk)
* [Reference Android SDK](https://github.com/matrix-org/matrix-android-sdk)
* [Reference iOS SDK](https://github.com/matrix-org/matrix-ios-sdk)
* [Python client SDK](https://github.com/matrix-org/matrix-python-sdk)

...and many many more: see https://matrix.org/blog/try-matrix-now for the full list of existing projects.


Potential GSoC ideas:
---------------------
Remember that you can also use these as inspiration and suggest your own project ideas.

## This is list is now prioritised - most important suggestions first (as of Feb 9th 2017)

### Building Bridges!

Bridging (linking existing networks into the wider Matrix ecosystem) is one of the most important bits of Matrix, and one of the most rewarding.  Right now we have bridges for:
 * Production grade:
  * IRC: https://github.com/matrix-org/matrix-appservice-irc
  * Slack: https://github.com/matrix-org/matrix-appservice-slack
  * Gitter: https://github.com/matrix-org/matrix-appservice-gitter
 * Beta grade:
  * RocketChat: https://github.com/matrix-org/matrix-appservice-rocketchat
  * Verto (FreeSWITCH): https://github.com/matrix-org/matrix-appservice-verto
 * Alpha grade:
  * Telegram Client https://github.com/matrix-org/matrix-appservice-tg
  * Libpurple https://github.com/matrix-org/node-purple/tree/master/appservice
  * Asterisk https://github.com/matrix-org/matrix-appservice-respoke
 * And lots of experimental ones from the community: Twitter, XMPP, iMessage, Facebook Messenger, etc.
 * ...and the full list at https://matrix.org/blog/try-matrix-now under Application Services.

Bridges are relatively easy and fun to write, and we would *love* for GSOCers to get involved in writing new bridges and polishing the existing ones.

We are most interested in bridges for:
 * Libpurple - as if you can connect to libpurple, you can immediately connect to lots of other services.
 * Hangouts - there's a very simple PoC at https://github.com/CyrusTheHedgehog/Hangouts-Bridge using the hangups library - building a proper one would be great!
 * XMPP - there are some promising bridges, but none are comprehensive.  https://github.com/pztrn/matrix-xmpp-bridge is the most advanced, but there's still lots ot work to go to make it perfect
 * Discord - discord's API should make bridging quite easy, but nobody's written one yet!
 * Email - by the time GSoC comes around Matrix should have threading support.  Building email and bulletin board bridges would be a fantastic way to showcase threading.

By default our preferred language for writing bridges is in Node.js (ES6), so we can build on top of the https://github.com/matrix-org/matrix-appservice-bridge library which provides a bunch of useful infrastructure and boilerplate.  If the remote network lacks good Node library support we consider other languages though.

**Expected results**: Bridging matrix rooms and users into one or more of the above environments - ideally supporting dynamic users (i.e. auto-creating users on both sides of the bridge on demand) and dynamic rooms (i.e. bridging the whole namespace of the remote network into matrix).

**Difficulty**: Ranges from Easy through to Hard depending on the network!

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))



### Integrations to ALL THE THINGS!!

As well as bridging, we're building out a large ecosystem of integrations (also known as bots) to let folks interact with other services from Matrix.  Today this is mainly in Go, with https://github.com/matrix-org/go-neb being the flagship bot project.  However, there's also the python incarnation (https://github.com/matrix-org/Matrix-NEB) as well as Hubot adaptors like https://github.com/davidar/hubot-matrix and other bot frameworks like https://gitlab.com/argit/hello-matrix-bot.

Bots can be written in any language, and we have a wide range of SDKs already available to help people get up and running - from everything from Node to Python to Perl to Ruby to Elixir...

Platforms we'd love to integrate with via native Matrix bots include:
 * Trello bot
 * Twitter bot
 * Basecamp bot
 * IFTTT
 * Zapier
 * Nagios
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
 * Building UI modules for Riot to provide a 'conversational interface' UI onto the bots
 * Extending bots into bridges, where appropriate.

**Expected results**: Creating client-server API bots that respond to !-commands to interact with the given integrated services, and/or inject messages into rooms based on those services.

**Difficulty**: Ranges from Easy through to Medium depending on the service!

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Kegan Dougal ([github](https://github.com/Kegsay))


### Internationalising Matrix

None of the Matrix clients (still!) are currently internationalised.  This is a real shame, especially given that the core dev team is made up of many different nationalities (English, French, Norwegian, etc).  This would be an easy but very useful project to go through implementing consistent internationalisation support across all of our reference clients and servers, working with the wider Matrix open source community to source translations as required.

**Expected results**: Architectural support for i18n in all reference matrix clients and servers, and implementations of at least 4 languages (translation provided by the wider community).

**Difficulty**: Easy / Moderate

**Knowledge pre-req**: Basic Javascript, iOS, Android.

**Potential mentor**: David Baker ([github](https://github.com/dbkr))


### Adding end-to-end encryption to more clients

One of the big new features of Matrix in 2016 was launching End-to-End Encryption using the Olm & Megolm cryptographic ratchets, and getting it assessed by NCC Group - see https://matrix.org/blog/2016/11/21/matrixs-olm-end-to-end-encryption-security-assessment-released-and-implemented-cross-platform-on-riot-at-last/ for details.

However, the current implementation has only landed in matrix-js-sdk, matrix-ios-sdk and matrix-android-sdk.  As a result, any client or bridge or bot which isn't built on one of those codebases is currently out of luck.

In this project, you would port the application-layer E2E implementation to one or more other clients - e.g. to Golang for use with go-neb, or to Python for use with matrix-python-sdk or to C++ for libqmatrixclient (as used by the Quaternion & Tensor desktop clients) or to C for matrix-purple (as used by Pidgin).  Alternatively, you might consider implementing an E2E-aware matrix proxy which *any* client can connect to (when running locally) to share encrypted communication with the rest of Matrix.

This would be a great way to improve your cryptography skills and learn about one of the most exciting and ambitious E2E cryptography projects out there.

**Expected results**: Extend other Matrix clients to speak E2E, or implement an E2E-aware Matrix Proxy

**Difficulty**: Hard

**Knowledge pre-req**: Cryptography. The language for the platform you are targetting.

**Potential mentor**: Richard van der Hoff ([github](https://github.com/richvdh)), Matthew Hodgson ([github](https://github.com/ara4n))



### HTML Embeddable Matrix Chat Rooms

Blogs and articles that allow users to engage with the author and comment on the content are standard in today's web and hugely popular. The implementations of these are largely from the authors of the blog or often completely proprietary in the case of newspaper or magzine articles. If I comment on a article and start discussing it with someone else, I now have to keep going back to that article to continue the discussion.

Matrix could be used as a platform where users can arrive at a random website, sign in with their Matrix ID, comment on a blog post or article and then continue that discussion through a standard Matrix client.

**Expected Results**: Extending https://github.com/matrix-org/matrix-react-sdk to provide reusable web compoents that a website author can download, embed and skin into their website to make comments work with minimal work to integrate. Could require user to log in with a matrix account to post (so your Matrix account would let you post comments on any website which used this), or support anonymous guest access. The blog author would be able to add their own comments and moderate comments. VoIP and Video calling support would be an added bonus. Other extensions would be plugins for blogging platforms so users of WordPress or similar can use the software on their blogs by just installing the plugin.

There is some related prior art at https://live.hello-matrix.net/ and https://github.com/Half-Shot/matrix-gsoc-bark but neither of these are specifically for embedded rooms.

**Difficulty**: Easy/Moderate

**Knowledge pre-req**: HTML, Javascript

**Potential mentor**: David Baker ([github](https://github.com/dbkr)), Erik Johnston ([github](https://github.com/erikjohnston)), Kegan Dougal ([github](https://github.com/Kegsay))


### IPFS support for content repositories

Currently Matrix uses a basic distributed content repository based on replicating data over HTTPS between its servers.  It could be nice to support storing data in IPFS instead, providing dedicated p2p distributed immutable data storage rather than the stop-gap solution that Matrix provides.

**Expected Results**: Extend synapse to optionally store and load content from IPFS, and extend one or more matrix clients (e.g. Vector) to natively load/store content from IPFS clientside.

**Difficulty**: Medium

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))


### Matrix Visualisations

When developing on Matrix it's often quite hard to visualise the underlying replicated Directed Acyclic Graph datastructure that describes the conversation history in a room.  We've made some basic tools in the past like https://github.com/Kegsay/matrix-vis and https://github.com/matrix-org/synapse/tree/master/contrib/graph and https://github.com/erikjohnston/matrix-introspection but what would be really cool would be a real-time visualisation of the DAG to help folks understand Matrix, and help developers debug interesting edge cases and merge resolution scenarios when the DAG bifurcates.  This could be written in any language, talking some combination of the server-server API or an enhanced version of the client-server API or just inspecting your synapse's database to visualise what's going on.

**Expected results**: A realtime visualisation of the DAG of a given Matrix room, as seen from the perspective of one or more HSes.

**Difficulty**: Medium

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Erik Johnston ([github](https://github.com/ErikJohnston)) or Kegan Dougal ([github](https://github.com/Kegsay))


### Alternative Efficient Client-Server Transports and Encodings

Matrix's baseline Client-Server API is simple long-polling HTTP calls.  This is purely for compatibility and simplicity for the widest range of client devices and applications, however - we encourage and expect people to implement more efficient transports and encodings in future.  For instance, we've published and implemented a beta Websockets transport draft at https://github.com/matrix-org/matrix-doc/blob/master/drafts/websockets.rst and https://github.com/matrix-org/matrix-websockets-proxy.

It would be *really* fun to experiment with other transports and encodings to find just how fast, low latency, low CPU or low bandwidth one can make the Client Server API run.  This could involve playing around with COaP+CBOR, MQTT, protobufs, capnproto, messagepack, HTTP/2 or any other option in a quest for the holy grail transport/encoding combination!

**Difficulty**: Medium

**Knowledge pre-req**: Network protocols

**Potential mentor**: Richard van der Hoff ([github](https://github.com/richvdh))


### Finishing matrix-ircd

https://github.com/matrix-org/matrix-ircd is a new project that provides an IRC front-end to any Matrix homeserver, written in Rust, which means anyone can point their existing IRC clients into Matrix, treating as a giant distributed ircd.  This helps people get up and running in the Matrix ecosystem without having to jump all the way to a Matrix client (or bridge via an existing IRC network).  It's in early beta currently, but fun to hack on with lots of functionality still to be finished.

**Expected results**: Add features and stability to matrix-ircd and get irc.matrix.org running as an IRC interface into the guts of Matrix!

**Difficulty**: Easy to Moderate

**Knowledge pre-req**:  Basic Rust and familiarity with web services.

**Potential mentor**: Erik Johnston ([github](https://github.com/erikjohnston))


### Extending Native Matrix Desktop Clients

There are several native Matrix Desktop Clients in development...

 * NaChat (Qt + C++) https://github.com/Ralith/nachat
 * Quaternion (QML + C++) https://github.com/fxrh/quaternion
 * Tensor (QML + JS) https://github.com/davidar/tensor
 * Unplug (JavaFX + Kotlin) https://github.com/UprootLabs/unplug
 * MatrixClient (macOS + Swift) https://github.com/aapierce0/MatrixClient
 * Pidgin (glib + C + libpurple) https://github.com/matrix-org/purple-matrix 

 ...all of which could be extended further.  Developers wanting to improve and hack features into fun desktop clients would be welcome here!

**Expected results**: Add new features to NaChat, Quaternion, Tensor etc.

**Difficulty**: Easy to Moderate

**Knowledge pre-req**: Familiarity with web services, the language used for implementing the client (e.g. ObjectiveC, Java)

**Potential mentor**: Erik Johnston ([github](https://github.com/erikjohnston)), David Baker ([github](https://github.com/dbkr))



### Helping out on Ruma (Rust Homeserver)

Ruma (https://ruma.io) is a project from the community to implement a Matrix homeserver in Rust.  It's making solid progress, and would be great to have both client-side and server-side components for Matrix implemented in Rust, and there's a huge amount of work to be done there.

**Expected Results**: Extend Ruma's components to implement more Matrix endpoints.

**Difficulty**: Hard

**Knowledge pre-req**: Rust, Web Services

**Potential mentor**: Erik Johnston ([github](https://github.com/erikjohnston))



# Ideas below this point almost certainly require more effort than the GSoC format allows, but are included here for interest's sake.


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



### Matrix Virtual World

By integrating WebGL (e.g. using a library like ThreeJS) with Matrix, one can create a collaborative virtual world whose data is persisted in Matrix, replicated over all participating Matrix homeservers with no single points of control or failure.  If implemented as a generic platform, one could first start off by sharing 3D geometry in the world, and then defining higher level semantics (perhaps in combination with matrix Application Services) to define business logic for the world.  A good example could be building a collaborative 3D model editor on top of Matrix, or a 2D collaborative graphical programming environment.

**Expected results**: A WebGL Matrix client that renders 3D geometry described in Matrix, allowing direct manipulation and operational transforms for concurrent access.

**Difficulty**: Hard

**Knowledge pre-req**: 3D graphics, WebGL, Operational Transform theory all a plus.  Would likely require optimisations and/or extensions to the server to support storing object graphs in Matrix.

**Potential mentor**: Matthew Hodgson ([github](https://github.com/ara4n))

