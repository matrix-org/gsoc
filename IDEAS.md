Google Summer Of Code Matrix Ideas list
=======================================

What is Matrix?
---------------

Matrix is a global, federated network of servers that together become an eventually-consistent database, optimized for messaging data. Just like email, you can either run your own Matrix homeserver, which means you own and control your own communications and history - or you can use one hosted by someone else (e.g. matrix.org) - there is no single point of control or mandatory service provider in Matrix. In fact, there is no single point of control over conversations in Matrix at all - conversation history is a first class citizen, with room state replicated over all participating servers, avoiding single-points of failure or control as you get in XMPP MUCs.

You can also use matrix to send and receive other types of data - events are passed as JSON objects, so you can use Matrix to collect and broadcast IoT-type data, or program-specific data packets or other objects you need to send back and forth. Matrix itself is a spec, and you can write your own server or client by implementing the spec - we also have provided reference implementations of a [python server](https://github.com/matrix-org/synapse) and clients in [AngularJS](https://github.com/matrix-org/matrix-angular-sdk), [Android](https://github.com/matrix-org/matrix-android-sdk) and [iOS](https://github.com/matrix-org/matrix-ios-sdk).

This means that if you use Matrix as your communication protocol in two separate projects, you automatically gain inter-project communication support between these projects. In the end, we hope Matrix will crack the problem of a widely successful open federated platform for communication on the internet - you should be able to use your favourite app to communicate via Matrix - and your recipients should be able to reply through the app of their choice!

APIs and architecture:
----------------------
In Matrix, a user account belongs to a homeserver and looks like this: *@localpart:domain* - the localpart is the "username" and the domain is the homeserver on which the account belongs. In other words, *@user1:matrix.org* is a different user to *@user1:example.com* as they are registered on different homeservers. 

In the Matrix network, anyone can run a homeserver. Anyone can also run a client, and you can connect to any homeserver from any client.

A client typically represents a human using a web application or mobile app. Clients use the ["Client-to-Server" (C-S) API](https://github.com/matrix-org/matrix-doc/blob/master/specification/20_client_server_api.rst)  to communicate with their homeserver, which stores their profile data and their record of the conversations in which they participate.

A "homeserver" is a server which provides C-S APIs and has the ability to federate with other HSes via the [Federation API](http://github.com/matrix-org/matrix-doc/blob/master/specification/30_server_server_api.rst). It is typically responsible for multiple clients. "Federation" is the term used to describe the sharing of data between two or more homeservers.

Here is a diagram of this architecture:

                      How data flows between clients
                       ==============================
     
     { Matrix client A }                             { Matrix client B }
         ^          |                                    ^          |
         |  events  |                                    |  events  |
         |          V                                    |          V
     +------------------+                            +------------------+
     |                  |---------( HTTPS )--------->|                  |
     |   Home Server    |                            |   Home Server    |
     |                  |<--------( HTTPS )----------|                  |
     +------------------+        Federation          +------------------+


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
There are many minecraft clones available e.g. https://github.com/fogleman/Minecraft - but none of these are networked in any way. The aim of this project is to design and implement a protocol which can allow multiple minecraft players to play together, even though they are using different clients - by having the data communication go through Matrix.

**Expected results**: Able to have 2+ players building structures together

**Difficulty**: Hard. Getting sensible chunking algorithms for rooms is Hard. There is huge scope to build on this both feature wise (e.g. PvP, monster AI) and protocol wise (reliability, masking latency hiccups, etc)

**Knowledge pre-req**: Python (assuming fogleman/Minecraft is used as a base)

**Potential mentor**: Kegan Dougal
   

### Tumblr gateway
[Tumblr](http://tumblr.com) is a share-anything pubsub blog application. Tumblr has a public API which you can use to extract and submit posts. It would be great if you could join a room alias like #tumblr_username and see a complete feed of their posts in Matrix, optionally responding to them from any Matrix client. This can be done use the Application Services API in Matrix.

**Expected results**: Able to join a room alias for any tumblr user and see a feed (even if it's just text) of their posts. Bonus points for gifs/videos/etc, and the ability to post comments on the posts and/or reblog.

**Difficulty**: Moderate.

**Knowledge pre-req**: Good knowledge of HTTP/REST APIs in general.

**Potential mentor**: Kegan Dougal
    
### Etherpad clone
[Etherpad](http://etherpad.org/) is a multi-user, real-time text collaboration tool which we use frequently internally. The aim of this project is to recreate Etherpad using Matrix. As a start, aim for a multi-user "notepad"-style application, and then more advanced features (chat, per-user history, different fonts/text-effects/etc) can be added as extensions.

**Expected results**: Able to have at least 10 people collaborating (typing) on a single document, and to have the document in sync across all people.

**Difficulty**: Hard. Made harder by needing to storing and synchronising document snapshots efficiently

**Knowledge pre-req**: Python/Twisted for server-side extensions; Client-side development (Javascript/HTML/CSS or Android or iOS), HTTP/JSON APIs, basic awareness of Operational Transform theory

**Potential mentor**: Kegan Dougal

### Matrix Powered Microblogging
Matrix-powered, open and federated microblogging platform. Basically, implement something like [Twitter](http://twitter.com) in Matrix - users can post updates and follow each other, and subscribers get a feed of the users they follow. The great thing with using Matrix for something like this, is that other clients can view and respond to updates from the microblogging application - as long as the common Matrix message types are used.

**Expected results**: User can log in, choose some users to follow, get an aggregated feed of 'tweets' from users they follow, and post 'tweets'.  Messages should be sendable and consumable by both generic Matrix clients as well as the microblog-specific optimised user experience. A web client would probably be the standard with mobile clients as extensions.

**Difficulty**: Moderate

**Knowledge pre-req**: HTML, CSS, Javascript

**Potential mentor**: David Baker

### Location based Chat
A mobile app that shows you a list of chat rooms "around you". People could create chat rooms fixed in one place (a Café could have a room, for example) or you could create a chat room that follows you around as you walk around using the app. Perhaps users could also see other users around them and create chats with them if they had the app open, or see what other chats they were in.

Some level of moderation would likely be necessary - this could be a natural extension once the base features have been implemented. 

A lot of code for the chat itself can be implemented with reusable UI components of the Matrix Console apps. It should be relatively straightforward to allow users to post pictures, video and audio clips to the room using standard Matrix message types and reusable components. 

**Expected Results**: An app and backend where you can log in, create a room, find and join rooms near you and chat.

**Difficulty**: Moderate

**Knowledge pre-req**: Android/iOS, probably python and SQL for the backend.

**Potential mentor**: David Baker (iOS), Kegan Dougal (Android)

### HTML Embeddable Matrix Chat Rooms
Blogs and articles that allow users to engage with the author and comment on the content are standard in today's web and hugely popular. The implementations of these are largely from the authors of the blog or often completely proprietary in the case of newspaper or magzine articles. If I comment on a article and start discussing it with someone else, I now have to keep going back to that article to continue the discussion.

Matrix could be used as a platform where users can arrive at a random website, sign in with their Matrix ID, comment on a blog post or article and then continue that discussion through a standard Matrix client.

**Expected Results**: A javascript/HTML SDK of some form that a website author can download, embed and skin into their website to make comments work with minimal work to integrate. Could require user to log in with a matrix account to post (so your Matrix account would let you post comments on any website which used this). The blog author would be able to add their own comments and moderate comments. VoIP and Video calling support would be an added bonus. Other extensions would be plugins for blogging platforms so users of WordPress or similar can use the software on their blogs by just installing the plugin.

**Difficulty**: Easy/Moderate

**Knowledge pre-req**: HTML, Javascript

**Potential mentor**: David Baker, Erik Johnston

### Clustered Homeservers
Whilst Matrix itself is a global eventually consistent database, the current server implementations have no horizontal scaling or high availability per homeserver node.  As a result, it's impossible for a single homeserver to scale beyond a single core currently.  This project would extend the Synapse (Python) or Pallium (Golang) homeserver implementations to support simple clustering by letting the multiple instances run concurrently, sharing distributed state over the network such that clients can connect to arbitrary nodes within the cluster.

**Expected Results**: Clients can connect per-request to one of many active/active nodes in the same homeserver cluster, and experience a consistent view of the homeserver state.  Nodes may fail in the cluster without impacting client experience.

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Python/Twisted or Golang.  Experience of clustering strategies a plus.

**Potential mentor**: Erik Johnson, Mark Haines

### Golang Matrix Homeserver
The reference implementation of the Matrix homeserver is currently Synapse, written in Python.  There also exists a 3rd party implementation written in Golang called Pallium (http://github.com/KoFish/pallium), which is promising but lacks support for the Federation API, recent Client-Server API features and generally needs more polish.  The code is a good basis for future work however and building it out to support basic federation would be an incredibly worthwhile project.

**Expected Results**: Pallium has been extended to support the new v2 CS-API and can also talk to other servers via the Federation API.

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Some knowledge of Golang

**Potential mentor**: TBD

### Arbitrary SQL backend support in Synapse
The Synapse python homeserver reference implementation is currently hardcoded to use sqlite as a database.  Whilst this simplifies setup and is okay for light-medium performance, it rapidly becomes a bottleneck for larger deployments because of sqlite's inherently single-threaded nature.  It also kills the possibility of HA at the database layer, or hosting the database on dedicated hardware.   The aim here is to modify Synapse's storage layer to support arbitrary SQL dialects by manipulating the current 'generic SQL' statements into dialect-specific ones, either using an existing library or manual extensions to the current database abstraction layer.

**Expected Results**: Synapse supports multiple SQL backends - at least MySQL or Postgres.  Crate.io for bonus points (if it makes sense).

**Difficulty**: Easy/Moderate

**Knowledge pre-req**: Some python & SQL knowledge desirable

**Potential mentor**: Erik Johnston

### Libpurple Matrix Plugin
The Matrix ecosystem has relatively few clients currently (just AngularJS, iOS, Android and two alpha commandline clients).  Implementing a libpurple module that talks the Matrix Client-Server REST API would improve things enormously, letting clients like Pidgin and Adium speak through to Matrix as well as bridges like Bitlbee.  The catch is that the libpurple architecture is focused around message passing rather than history synchronisation like Matrix, so there will be a bit of an impedence mismatch between the libpurple API and the Matrix Client-Server API. This should be solvable however, just as libpurple supports MUC history playback for XMPP.  An extension idea could include wrapping the resulting plugin in haze for use in empathy.

**Expected Results**: Any libpurple-backed IM client can connect to a Matrix homeserver to send/receive IMs and other content.

**Difficulty**: Moderate

**Knowledge pre-req**: Good C skills and HTTP API knowledge. Glib knowledge an added bonus.

**Potential mentor**: Erik Johnston

### Command line Matrix client
A recurring request from poweruser newcomers to Matrix is whether we have any command-line clients.  Creating a new commandline client implementation (perhaps combined with the libpurple plugin mentioned above), or implementing an irssi plugin, or weechat or similar would be really useful.

**Expected results**: A new commandline/text-user-interface Matrix client implementation that can support textual groupchat modes of communication in Matrix.

**Difficulty**: Moderate

**Knowledge pre-req**: Familiarity with the language used to implement the client would be a bonus.  Understanding of HTTP API basics a must.

**Potential mentor**: Erik Johnston

### Add Matrix into Known
Withknown.com is a new opensource distributed social network and blogging platform written in PHP, following the "wordpress" model.  We think it would be really cool to embed Matrix clients into the Known web engine, providing the equivalent functionality to Known that FB Messenger provides to Facebook.  Just as Known users can host their own Known servers, they could also be able to host their own Matrix servers, and use them for all their social messaging and video/voice calling needs from the comfort of their own website.  This project is tightly coupled to the "HTML Embeddable Matrix Chat Rooms" project mentioned above.

**Expected results**: Known PHP module for embedding matrix clients into Known websites.

**Difficulty**: Moderate

**Knowledge pre-req**: Familiarity with PHP, HTML, CSS, and HTTP APIs.

**Potential mentor**: Erik Johnston

### Matrix Gateways
Matrix's Application Service API provides a simple but powerful way to build arbitrary application logic on top of Matrix - e.g. gateways between Matrix and other communication environments such as SIP, IRC, XMPP, Lync, and proprietary chat/VoIP services.  This project would be to pick a common existing communication protocol (e.g. XMPP) and build an Application Service which bridges it into Matrix - thus extending both ecosystems, supporting as high a common set of capabilities as possible (e.g. VoIP if available, group chat if available, synchronised history if available etc).  The service could be built on our existing reference Python implementation Application Server framework.  An interesting extension would be to support end-to-end encryption over a federation - e.g. federating TextSecure's reference server with Matrix (Matrix's end-to-end encryption should be compatible with Axolotl, the algorithm TextSecure uses).

**Expected results**: An application service which provides two-way bridging of group and 1:1 chat, including masquerading 'foreign' users and rooms into Matrix.

**Difficulty**: Moderate
Knowledge pre-req: Familiarity with web services, the language used for implementing the service (e.g. Python if using our reference example service framework) and the protocol being bridged.

**Potential mentor**: TBD

### Native Matrix Desktop Client
We currently have no dedicated desktop GUI Matrix clients at all.  There have been many requests for a richer non-HTML client for desktop use - either porting the opensource iOS app to run on OSX, or using the Java SDK to implement a JavaFX application or similar.

**Expected results**: a desktop GUI Matrix client supporting basic group chat functionality.

**Difficulty**: Moderate

**Knowledge pre-req**: Familiarity with web services, the language used for implementing the client (e.g. ObjectiveC, Java)

**Potential mentor**: Erik Johnston (Not objective c)

### Matrix<->Blog bridge and client
Related to the "Tumblr gateway" idea suggestion - rather than just bridging content from Tumblr into Matrix, one could build a 'communication dashboard' app which aggregates content and comments from a wide range of blogs, messageboards, forums etc and presents them in a single interface - much like an RSS aggregator.  Unlike an RSS aggregator one could also post comments and answers directly from within the dashboard via Matrix, using a generic blog<->Matrix application service gateway.  This could put provide a consistent open decentralised API to all conversations on the the internet, with no single points of control.

**Expected results**: A two-way conversation dashboard client and accompanying Matrix Application Service which allows 

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Familiarity with web services, the language used for implementing the service (e.g. Python if using our reference example service framework), and the language used for implementing the dashboard app/website (e.g. AngularJS/JQuery/Javascript/HTML/CSS).

**Potential mentor**: TBD

### Threaded Matrix client
One of the major early uses of Matrix are public rooms (similar to IRC) focused around given topics, for example Matrix support channel, android development, etc. These run into the classic problem of having multiple concurrent conversations in them, which often leads to confusion for all participants. One of the desired features of Matrix is to provide threading support such that individual messages can be marked as a reply to others, this would allow apps to differentiate the various different conversations in the UI giving a much better and more usable user experience.
This project would involve helping to finalize how Matrix supports threading, as well as implementing support in one or more of the current clients.

**Expected results**: A client with support for replying to particular messages and showing the ongoing and historic threads.

**Difficulty**: Moderate
Knowledge pre-req: Familiarity with at least one of the languages of the current clients (AngularJS, Android or Objective C)

**Potential mentor**: TBD

### Implementing WebRTC support in Mobile apps
As of the time of writing Matrix's mobile apps on iOS and Android don't support VoIP calling, which is a major shortcoming given Matrix's Client-Server HTTP API offers a simple pragmatic approach for federated WebRTC calling.  In this project, you would add a WebRTC stack to the iOS and/or Android applications (e.g. OpenWebRTC, or Google's WebRTC stack, or Google's in-built Android WebRTC stack) in order to support voice and video calling to the reference example Matrix clients.

**Expected results**: The reference iOS or Android matrix clients support VoIP and Video calling to other Matrix clients (e.g. the existing WebRTC support in the reference Matrix web client).

**Difficulty**: Moderate/Hard
Knowledge pre-req: Familiarity with iOS or Android development, and linking native 3rd party libraries into existing clients.  Basic knowledge of VoIP signalling an advantage, but not prerequisite.

**Potential mentor**: David Baker

### Multi-way voice and video conferencing
Matrix currently has one-to-one voice and video conferencing using WebRTC. This project would be to add multi-user voice and video chat to the Matrix web client. This would likley be done by extending a standard VoIP conferencing server such as Jitsi Video Bridge (https://jitsi.org/Projects/JitsiVideobridge). This would involve working with the Matrix team to extend to the Matrix specification as necessary to support conferencing and helping to define the open ecosystem for VoIP calls in the future. It will then involve the addition of Matrix support to the chosen conferencing server and the addition of UI to the web client to support it.

To start with, this project would support voice conferences so that users can speak together (without the speaker's voice being echoed back at them). The next step would be to add video support so the participants can all see each other.

The best solution here will balance quality and bandwidth usage, for example by using low-resolution video streams for participants that are not currently speaking and higher quality ones for active members, switching between them as required. Voice Activity Detection could be used to automatically focus the active speaker.

**Expected Results**: A Matrix web client where users can establish a multi-party voice / video conference call and server software to enable this as necessary, as well as input into the Matrix specification.

**Difficulty**: Hard

**Knowledge pre-req**: Javascript, HTML, CSS, WebRTC, some experience with real time audio and video. Java if Jitsi video bridge chosen.

**Potential mentor**: David Baker

### Matrix Search Engine
There is currently no way to index content in Matrix.  Luckily the Application Service API makes it trivial to query the conversation history of the public rooms on a given server, meaning that room history could easily be spidered and indexed into a search engine such as ElasticSearch.  A simple web interface could then provide a Google Groups-style search engine across all public accessible content in Matrix, if extended to support multiple homeservers.  A related extension could be implementing a search-engine friendly view layer on the default matrix webclient, allowing Google and other search engines themselves to directly index Matrix content.

**Expected results**: An application service that indexes homeserver content, and a web API and  interface for searching for given terms and viewing results.

**Difficulty**: Easy/Moderate

**Knowledge pre-req**: Familiarity with web services, the language used for implementing the application service (e.g. Python if using our reference example service framework).  Basic HTML/CSS/Javascript needed to implement the search engine interface frontend.

**Potential mentor**: TBD

### Collaborative Whiteboarding in Matrix
Matrix allows clients to send and synchronize arbitary pieces of data in a room, allowing the possibility collabrative editing. This project would be to use this ability to design and implement a collaborative whiteboarding app using Matrix. This is similar to the etherpad project above, except synchronizing a whiteboard canvas between clients instead of text.

**Expected results**: A client that supports allowing multiple users drawing and editing the whiteboard similutaneously, with the results synchronized in real time between all clients in the room.

**Difficulty**: Hard

**Knowledge pre-req**: Python/Twisted for server-side extensions; Client-side development (Javascript/HTML/CSS or Android or iOS), HTTP/JSON APIs, basic awareness of Operational Transform theory

**Potential mentor**: TBD

### Matrix Virtual World
This is an extension of both the etherpad, Matrixcraft and Collaborative whiteboarding ideas mentioned above.  By integrating WebGL (e.g. using a library like ThreeJS) with Matrix, one can create a collaborative virtual world whose data is persisted in Matrix, replicated over all participating Matrix homeservers with no single points of control or failure.  If implemented as a generic platform, one could first start off by sharing 3D geometry in the world, and then defining higher level semantics (perhaps in combination with matrix Application Services) to define business logic for the world.  A good example could be building a collaborative 3D model editor on top of Matrix, or a 2D collaborative graphical programming environment.

**Expected results**: A WebGL Matrix client that renders 3D geometry described in Matrix, allowing direct manipulation and operational transforms for concurrent access.

**Difficulty**: Hard

**Knowledge pre-req**: 3D graphics, WebGL, Operational Transform theory all a plus.  Would likely require optimisations and/or extensions to the server to support storing object graphs in Matrix.

**Potential mentor**: TBD

### Internationalising Matrix
None of the Matrix clients are currently internationalised.  This is a real shame, especially given that the core dev team is made up of many different nationalities (English, French, Norwegian, etc).  This would be an easy but very useful project to go through implementing consistent internationalisation support across all of our reference clients and servers, working with the wider Matrix opensource community to source translations as required.

**Expected results**: Architectural support for i18n in all reference matrix clients and servers, and implementations of at least 4 languages (translation provide by the wider community)

**Difficulty**: Easy

**Knowledge pre-req**: Basic Javascript, iOS, Android.

**Potential mentor**: TBD

###Matrix Client UI/UX improvements
None of the reference Matrix clients have ever had any professional graphical design or user interface/user experience support.  This is partially deliberate, as our focus has been entirely on the technical implementation of the overall platform, and we don't want to put other people off building glossy Matrix-power apps.  In practice, it does turn people off Matrix as a whole, and we don't want to be responsible for creating bad UX.  So if you are an aspiring UX/UI designer, we would love you to come attack our reference clients and work with the dev team to implement your dreams of the ultimate communication tool!

**Expected results**: improved and consistent skins or UX across the Matrix reference clients

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: UX/UI design skills; Photoshop or equivalent for building pixel-perfect UIs which the dev team can then go implement.

**Potential mentor**: TBD

### Music jamming over Matrix
The Matrix team built a "MIDI over Matrix" proof of concept called RemoteJam for TechCrunch Disrupt London 2014 - this was a simple Network MIDI to Matrix bridge which persisted network MIDI traffic into Matrix, and then transcribed it using javascript to musical notation  This project would extend or reimplement this hack to build a full remote musical jamming solution for Matrix, with no single points of failure or ownership over the resulting music.  Users anywhere on the net would be able to play together via MIDI, storing the data into Matrix for posterity and letting the public listen and view the transcription in realtime.

**Expected results**: one remote jamming web application powered by Matrix, and a MIDI<->Matrix bridge

**Difficulty**: Moderate/Hard

**Knowledge pre-req**: Some knowledge of MIDI and music useful.  Javascript/HTML5/AngularJS/CSS for the web application.  Python or similar for the basis MIDI<->Matrix application service bridge.  Knowledge of statistics useful for understanding quantising algorithms for transcribing MIDI.

**Potential mentor**: TBD

### IoT Dashboard with Matrix
Matrix is ideal as a platform for the Internet of Things: simple, federated, persistant communication would allow devices and hubs to communicate with services and one another in a unified, open and extensible way. IoT devices and hubs could send their data into Matrix which would distibute and store it as necessary. This project would involve input into a set of standards for such devices to put data into Matrix as well as client of some kind for visualising, analysing and orchestrating the data from these devices and potentially interacting with them. This could take the form of a webapp which reads the data from Matrix (using the angular SDK) and/or similar mobile clients. The client would display a list of all of my devices that were feeding data into the system and a summary of the data they're sending, allowing me to view a summary of recent data or get more detail and potentially plot graphs of the data from devices (for example, the curent temperature of my home thermostat and its trend over the last month). It's important that the system is open and usable by others, so specifying a format for data that's as flexible as possible whilst also providing rich, detailed information from each type of device would be an interesting problem.

**Expected results**: one IoT dashboard web application, with some IoT devices integrated via the Matrix client-server API.  Optionally also IoT application services for analysing/aggregating/visualising the resulting IoT data en mass.

**Difficulty**: Moderate

**Knowledge pre-req**: Javascript/HTML5/AngularJS/CSS for web application.  Python or similar for IoT application services if using our reference application service framework.

**Potential mentor**: TBD
