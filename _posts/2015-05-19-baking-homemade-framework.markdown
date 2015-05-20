---
layout:     post
title:      "Baking our CSS homemade framework"
categories:
  - general
  - front
  - design
author:     gabrielcousin
---

2015 has started with some ambitious projects! We released [Solid](http://getsolid.io)'s second version with a design reviewed from top to bottom. Also, we keep shiping new features like Office 365 support or like assigning actions which is coming in the following days.

This second iteration was the occasion for our designers to create a UI kit, the basis of our framework: [Tapestry](http://wisembly.github.io/tapestry). It is available on [GitHub](http://github.com/wisembly/tapestry) and as a Bower component.

At the moment, it contains UI elements needed in Solid. We recently added icons. That is why our older repo is not available any more, but the workflow used to build icons is included in Tapestry. We are currently on adding it into Wisembly and it is quite a big step. We are facing some difficulties. We built Tapestry with rems and we still have to support IE8, which doesn't deal with it… But still, it is a great opportunity to get rid of a lot of legacy code (Wisembly is almost 5!) and to optimize the front-end. I guess we can discuss these two topics later ;)