---
name: "HTML Embeddable Matrix Chat Rooms"
desc: "Create an embeddable component backed by a Matrix-room"
difficulty: "Medium"
issues:
mentors:
 - dbkr
initiatives:
 - GSoC
tags:
 - New Features
 - Riot
 - Client
---

Blogs and articles that allow users to engage with the author and comment on the content are standard in today's web and hugely popular. The implementations of these are largely from the authors of the blog or often completely proprietary in the case of newspaper or magzine articles. If I comment on a article and start discussing it with someone else, I now have to keep going back to that article to continue the discussion.

Matrix could be used as a platform where users can arrive at a random website, sign in with their Matrix ID, comment on a blog post or article and then continue that discussion through a standard Matrix client.

#### Expected Results

Extending https://github.com/matrix-org/matrix-react-sdk to provide reusable web compoents that a website author can download, embed and skin into their website to make comments work with minimal work to integrate. Could require user to log in with a matrix account to post (so your Matrix account would let you post comments on any website which used this), or support anonymous guest access. The blog author would be able to add their own comments and moderate comments. VoIP and Video calling support would be an added bonus. Other extensions would be plugins for blogging platforms so users of WordPress or similar can use the software on their blogs by just installing the plugin.

There is some related prior art at https://live.hello-matrix.net/ and https://github.com/Half-Shot/matrix-gsoc-bark but neither of these are specifically for embedded rooms.

#### Knowledge pre-req

HTML, Javascript