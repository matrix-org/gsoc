---
name: Tackle a meta issue in kazv
desc: Add more features to kazv to make it more usable
# add a short one line description of your project
requirements:
# Student requirements:
 - C++ or JavaScript
 - Knowledge of Qt, Qml and kde frameworks is a plus
 - Use, or be willing to use GNU/Linux (e.g. Ubuntu) or musl/busybox Linux (e.g. Alpine)
difficulty: medium
issues:
# Related issues (if any)  to this project.
 - https://lily.kazv.moe/kazv/kazv/-/issues/17
 - https://lily.kazv.moe/kazv/kazv/-/issues/18
 - https://lily.kazv.moe/kazv/kazv/-/issues/20
 - https://lily.kazv.moe/kazv/kazv/-/issues/19
 - https://lily.kazv.moe/kazv/kazv/-/issues/5
mentors:
# First person in contact; mentors may change before project starts.
 - tusooa
initiatives:
 - GSoC
tags:
 - 175h
# Different technologies needed
 - c++
 - cpp
 - javascript
 - GNU/Linux
 - qt
 - qml
 - kde frameworks
---


#### Description

[kazv][kazv] is a matrix client that aims to be convergent. It currently supports some features such as 
basic message handling and end-to-end encryption, but more features are missing. In this project you
would add some set of related features to kazv. They are grouped under the so-called `meta` issues.

You do not need to resolve a whole meta issue; you can choose to do only a part of them that fits your
schedule, but you do need to write in your proposal what features you plan to add, and relevant time
frames. If you feel a feature in other meta issues is a dependency of what you would like to do, you
can also add it to your plans, but be aware of the time limits of GSoC.

We use a self-hosted GitLab instance to track our [source code][proj-kazv]. You should make merge requests
to our repositories there. If you have issues cloning the repos (for example, if you do not 
have a reliable Internet connection to our servers), or do not want to reveal your email address for
GitLab registration, or have any other concerns about the project, please do not hesitate to contact me for help.

The matrix room for the Kazv Project is [#kazv:tusooa.xyz][mx-room]. You can contact me in that room,
or on <https://lily.kazv.moe> . Contacting me via GitHub is *discouraged*, as I do not check GitHub
regularly.

[mx-room]: https://matrix.to/#/#kazv:tusooa.xyz?via=tusooa.xyz&via=matrix.org&via=kde.org
[kazv]: https://lily.kazv.moe/kazv/kazv
[proj-kazv]: https://lily.kazv.moe/kazv

#### Milestones

##### GSOC CODING STARTS

* Be familiar with the Kazv Project
* Read the [matrix specs][spec], especially [client-server API][csapi]
* Compile kazv, along with its dependencies, from your side
* Start doing some features you planned (in your proposal, please write in detail what features you plan to add in each period)
* Create a merge request for each one you finished

[spec]: https://spec.matrix.org/v1.2/
[csapi]: https://spec.matrix.org/v1.2/client-server-api/

##### GSOC MIDTERM

* Finish some, and start doing other features you planned (in your proposal, please write in detail what features you plan to add in each period)

##### GSOC FINAL

* Make all merge requests you created ready for review
