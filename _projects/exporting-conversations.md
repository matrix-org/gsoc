---
name: Exporting Conversations
desc: Add support for exporting conversations from Element in a variety of formats.
# add a short one line description of your project
requirements:
# Student requirements:
 - Understanding of Matrix fundamentals such as rooms & events
 - Familiarity with Web technologies
difficulty: medium
issues:
# Related issues (if any)  to this project.
 - https://github.com/vector-im/element-web/issues/2630
mentors:
# First person in contact; mentors may change before project starts.
 - Michael (t3chguy)
initiatives:
 - GSoC
tags:
# Different technologies needed
 - TypeScript
 - ES6
---
This is an awesome project idea.

#### Description

Whilst Matrix & Element are obviously great,
sometimes you need to export your chat history
to share with outsiders, for print, or archival
purposes. Encryption makes this even harder as
you can't just simply and safely run an external
tool for this.
https://github.com/russelldavies/matrix-archive/
is such an existing tool but this is not massively
user friendly.

In this project you would add the ability for Element
to be able to export chat history for a given room &
period of time into a format (or formats) of your choosing.

#### Milestones

##### GSOC CODING STARTS

* Plan which output formats to implement
* Plan what the code will do

##### GSOC MIDTERM

* Write up a simple export tool for the chosen format for a single room which only considers the loaded timeline

##### GSOC FINAL

* Extend the implementation to support going back until a chosen start date to export a longer period of time

##### Stretch Goals

* Multiple output formats
