Google Summer Of Code Matrix Ideas list
=======================================

What is Matrix?
---------------

Matrix is a global, federated network of servers that together become an eventually-consistent database, optimized for messaging data. Just like email, you can either run your own Matrix homeserver, which means you own and control your own communications and history - or you can use one hosted by someone else (e.g. matrix.org) - there is no single point of control or mandatory service provider in Matrix. In fact, there is no single point of control over conversations in Matrix at all - conversation history is a first class citizen, with room state replicated over all participating servers, avoiding single-points of failure or control as you get in XMPP MUCs.

You can also use matrix to send and receive other types of data - events are passed as JSON objects, so you can use Matrix to collect and broadcast IoT-type data, or program-specific data packets or other objects you need to send back and forth. Matrix itself is a spec, and you can write your own server or client by implementing the spec - we also have provided reference implementations of a [python server](https://github.com/matrix-org/synapse) and clients in [AngularJS](https://github.com/matrix-org/matrix-angular-sdk), [Android](https://github.com/matrix-org/matrix-android-sdk) and [iOS](https://github.com/matrix-org/matrix-ios-sdk).

This means that if I use Matrix as my communication protocol in two separate projects, I automatically gain inter-project communication support between these projects. In the end, we hope Matrix will crack the problem of a widely successful open federated platform for communication on the internet - you should be able to use your favourite app to communicate via Matrix - and your recipients should be able to reply through the app of their choice!

APIs and architecture:
----------------------
In Matrix, a user account belongs to a homeserver and looks like this: *@localpart:domain* - the localpart is the "username" and the domain is the homeserver on which the account belongs. In other words, *@user1:matrix.org* is a different user to *@user1:example.com* as they are registered on different homeservers. 

In the Matrix network, anyone can run a homeserver. Anyone can also run a client, and you can connect to any homeserver from any client.

A client typically represents a human using a web application or mobile app. Clients use the ["Client-to-Server" (C-S) API](https://github.com/matrix-org/matrix-doc/blob/master/specification/20_client_server_api.rst)  to communicate with their homeserver, which stores their profile data and their record of the conversations in which they participate.

A "homeserver" is a server which provides C-S APIs and has the ability to federate with other HSes via the [Federation API](http://github.com/matrix-org/matrix-doc/blob/master/specification/30_server_server_api.rst). It is typically responsible for multiple clients. "Federation" is the term used to describe the sharing of data between two or more homeservers.

For a diagram of this architecture, see the ["How data flows between clients"](https://github.com/matrix-org/matrix-doc/blob/master/specification/00_basis.rst#51architecture) diagram in the [specification](https://github.com/matrix-org/matrix-doc/blob/master/specification/).


Code repositories:
------------------
Eveything is stored under [https://github.com/matrix-org](https://github.com/matrix-org/), e.g.:
* [Reference python server](https://github.com/matrix-org/synapse)
* [Reference AngularJS client and SDK](https://github.com/matrix-org/matrix-angular-sdk)
* [Reference Android client and SDK](https://github.com/matrix-org/matrix-android-sdk)
* [Reference iOS client and SDK](https://github.com/matrix-org/matrix-ios-sdk)
* [Python client SDK](https://github.com/matrix-org/matrix-python-sdk)

Potential GSoC ideas:
---------------------
Remember that you can also use these as inspiration and suggest your own project ideas.

### Matrixcraft

There are many minecraft clones available e.g. [https://github.com/fogleman/Minecraft](https://github.com/fogleman/Minecraft) - but none of these are networked in any way. The aim of this project is to design and implement a protocol which can allow multiple minecraft players to play together, through Matrix.

**Expected results**: Able to have 2+ players building structures together

**Difficulty**: Hard. Getting sensible chunking algorithms for rooms is Hard. There is huge scope to build on this both feature wise (e.g. PvP, monster AI) and protocol wise (reliability, masking latency hiccups, etc)

**Knowledge pre-req**: Python (assuming fogleman/Minecraft is used as a base)

**Potential mentor**: Kegan Dougal
   

### Tumblr gateway
Tumblr has a public API which you can use to extract and submit posts. It would be great if you could join a room alias like #tumblr_username and see a complete feed of their posts in Matrix, optionally responding to them from any Matrix client. This can be done use the Application Services API in Matrix.

**Expected results**: Able to join a room alias for any tumblr user and see a feed (even if it's just text) of their posts. Bonus points for gifs/videos/etc, and the ability to post comments on the posts and/or reblog.

**Difficulty**: Moderate.

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Kegan Dougal
    
### Etherpad clone
  Etherpad allows real-time text collaboration and we use it frequently internally. The aim of this project is to recreate Etherpad using Matrix.

**Expected results**: Able to have at least 10 people collaborating (typing) on a single document, and to have the document in sync across all people.

**Difficulty**: Hard. Made harder by needing to storing and synchronising document snapshots efficiently

**Knowledge pre-req**: Python/Twisted for server-side extensions; Client-side development (Javascript/HTML/CSS or Android or iOS), HTTP/JSON APIs, basic awareness of Operational Transform theory

**Potential mentor**: Kegan Dougal

### Matrix Powered Microblogging
Matrix-powered, open and federated microblogging platform.

**Expected results**: User can log in, choose some users to follow, get an aggregated feed of 'tweets' from users they follow, and post 'tweets'.  Messages should be sendable and consumable by both generic Matrix clients as well as the microblog-specific optimised user experience.

**Difficulty**: Moderate

**Knowledge pre-req**: HTML, CSS, Javascript

**Potential mentor**: David Baker

### Location based Chat
A mobile app that shows you a list of chat rooms "around you". People could create chat rooms fixed in one place (a Café could have a room, for example) or you could create a chat room that follows you around as you walk around using the app.

**Expected Results**: An app and backend where you can log in, create a room, find and join rooms near you and chat.

**Difficulty**: Moderate

**Knowledge pre-req**: Android/iOS, probably python and SQL for the backend.

**Potential mentor**: David Baker (iOS), Kegan Dougal (Android)

### HTML Embeddable Matrix Chat Rooms
A Matrix-powered engine for comments boxes.

**Expected Results**: A javascript/HTML SDK of some form that a website author can download, embed and skin into their website to make comments work with minimal work to integrate. Could require user to log in with a matrix account to post (so your Matrix account would let you post comments on any website which used this).  VoIP and Video calling support would be an added bonus.

**Difficulty**: Easy/Moderate

**Knowledge pre-req**: HTML, Javascript

**Potential mentor**: David Baker

### Clustered Homeservers
Whilst Matrix itself is a global eventually consistent database, the current server implementations have no horizontal scaling or high availability per homeserver node.  As a result, it's impossible for a single homeserver to scale beyond a single core currently.  This project would extend the Synapse (Python) or Pallium (Golang) homeserver implementations to support simple clustering by letting the multiple instances run concurrently, sharing distributed state over the network such that clients can connect to arbitrary nodes within the cluster.

**Expected Results**: Clients can connect per-request to one of many active/active nodes in the same homeserver cluster, and experience a consistent view of the homeserver state.  Nodes may fail in the cluster without impacting client experience.

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Python/Twisted or Golang.  Experience of clustering strategies a plus.

**Potential mentor**: Erik Johnson

