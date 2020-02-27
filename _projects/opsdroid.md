---
name: Enabling End to End Encryption in Opsdroid
desc: Opsdroid is a Python bot framework, by transitioning the matrix connector to use matrix-nio e2ee support can be added.
requirements:
 - Python
difficulty: low
issues:
 - https://github.com/opsdroid/opsdroid/issues/992
mentors:
 - Cadair
 - SolarDrew
 - jacobtomlinson 
initiatives:
 - GSoC
tags:
 - Python
 - asyncio
collaborating_projects:
 - opsdroid
---

#### Description

Opsdroid is a bot framework which works with many chat services, such as matrix, slack, telegram.
It aims to have a very low barrier to entry and be very user friendly.
The support for these different services are implemented in modules named "connectors", the matrix connector currently uses an [asyncio wrapper](https://github.com/Cadair/matrix_api_async) around the [matrix-python-sdk](https://github.com/matrix-org/matrix-python-sdk).
This SDK is largely unmaintained and a more modern Python SDK [matrix-nio](https://github.com/poljar/matrix-nio) has been created in that time, which powers projects like [pantalaimon](https://github.com/matrix-org/pantalaimon/) and [weechat-matrix](https://github.com/poljar/weechat-matrix).
As well as being a more modular SDK with pluggable IO support, this SDK also has well tested and complete end to end encryption support, which would be a great addition to opsdroid.


The main component of this project would be to transition the opsdroid matrix connector to use matrix-nio and update all tests, documentation and official skills to use the new APIs.
Having achieved this, you should write a how to get started with opsdroid and matrix in an accessible guide, with an introduction to using end to end encryption.

In addition to this there are multiple other ways the matrix support in opsdroid could be extended, some ideas (in increasing order of complexity) are:

* Update [database-matrix](https://github.com/solardrew/database-matrix) to use matrix-nio and integrate it into core.
* Support .well-known lookups for the client-server API endpoint.
* Support room upgrades.
* Add support for sending and receiving all common matrix event types.
* Improving user documentation of how different events are handled [#1293](https://github.com/opsdroid/opsdroid/issues/1293).
* Develop a scheme for device verification with the bot user.
* Develop a matrix connector which can utilise the appservice API.


#### Milestones

Below is an example timeline for this project, it prioritises the matrix-nio transition and does a couple of extra improvements after that.

##### Before GSOC

* Get familiar with the opsdroid codebase, make a Pull Request and write a skill.

##### GSOC CODING STARTS

* Transition the connector code over to `matrix-nio`.
* Work through the unit tests to update them for the new library, improving them as you go.

##### GSOC MIDTERM

* Update and integrate [database-matrix](https://github.com/solardrew/database-matrix) into core.
* Documentation, covering docstrings in the connector, narrative documentation in opsdroid and guides for the opsdroid or matrix.org website.

##### GSOC FINAL

* Add more events to the matrix connector.
* Add support for well-known lookups.
