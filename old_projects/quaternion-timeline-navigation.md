---
name: Better timeline navigation in Quaternion
desc: Introduce new ways of moving around vast numbers of events in the timeline
requirements:
 - QML
 - Understanding of usability (UI design/UX) concepts
 - C++11 (desirable)
difficulty: low to average
issues:
 - TBD
mentors:
 - KitsuneRal
initiatives:
 - GSoC
tags:
 - Qt
 - QML
 - GUI
---

#### Description

Traditional scrollbars don't work well with extremely long (1000's of events)
timelines: they don't guide you across days, periods of more active and less
active conversation. They also have another technical issue: since events are
usually rendered dynamically, the timeline "canvas" constantly changes its
height, leading to erratic movements of the scrollbar. One of desktop clients,
Quaternion, has an unconventional navigation control - shuttle dial - to deal
with the latter problem; but it still doesn't address the former one. This
project is an opportunity to work out a way to efficiently move around long
timelines without resorting to hit-and-miss clicks on the scrollbar.
If successful, the result may become a source of inspiration not only for other
Qt-based clients (NeoChat, Nheko) but also web-based ones, such as Element!

#### Milestones

##### GSOC CODING STARTS

* Get acquainted with the problem and map out possible research areas
* Investigate available prior art in navigating long feeds.

##### GSOC MIDTERM

* Implement a proof of concept for the navigation control.

##### GSOC FINAL

* Complete implementation of the navigation control within Quaternion.
