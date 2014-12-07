---
layout:     post
title:      "What we've learn from Ember.js after 2 months developing our new product. A Solid story"
categories:
  - general
author:     guillaumepotier
---

Here [@Wisembly](http://wisembly.com) we strive to change the way people meet, work and collaborate during meetings. We come from a Symfony2 / Backbone.js / socket.io world with our event / training / conf call products, and when it came to thinking about our next product, [Solid](http://getsolid.io), we slowed down things a bit and looked for maybe a different and possibly better way to manage our frontend application.

We looked at [Angular.js](https://angularjs.org/) and [Ember.js](http://emberjs.com/) that were trending among cool kids out there and that looked both promizing for us to manage an ambitious javascript application with our growing developpers team (by the way, [we are hiring!](http://wisembly.com/jobs)).

After doing the famous [Todo MVC example](http://todomvc.com/) and some other POCs, we decided to go for Ember with [Ember-cli](http://www.ember-cli.com/).

Here is ou real life Ember.js feedback, what we learnt, what we think it is cool, what is really uncool and what could be improved. Let's start.

## Ember

### Convention over configuration
**Ember is not like Backbone. It's not a library, it's a framework.**

That mean devs accepting to embrace Ember's philosophy will be greatly rewarded by the framework, whereas more reserved ones will suffer from fighting against concepts they may consider as very odd.

At the beginning, Ember is deep and obscure, it's like jumping in a gulf, blindfolded, and being turned back. But step after step, as conventions are understood and accepted, you discover how powerful it is, and how easily you can manage to make it perform very advanced tasks, very easily. Be be warned that your neurons will be shaken

#### What does that mean for scaling ?
Using these conventions means that you will continue to use them as your app and team grows up.

**Concerning the app:**

The complexity you felt in your first days has been transformed into concepts you have integrated, so your app's complexity will grow faster than your code's complexity => that's good for scaling !!!


#### What does that mean for your team

**Good points**
- Concerning your current team members, they will tend to produce more homogeneous code, and that's a great thing for productivity and comprehension
- That leads to the second good point. New team members understanding Ember will understand your code.

**Risks**
- What happens if you integrate an "Angular" dev ? It's very possible, since this framework is far more "hype" at the moment than Ember. Despite the fact that Ember and Angular are different in some ways, their concepts doesn't seem that far, and the new "dev on the block" should feel at home within days (1-2 weeks max.)
- You should consider understanding and using "the ember way" to do things, before trying to customize them => Think about tests, future upgrades, and glitches you should introduce in the app because "Hell yeah, i like to customize ALL THE THINGS"

### The world is made of components
Do you embrace DRY methodology ? Components are your new little friends ;)

Ember.js allows you to wrap all of your repeated pieces of code inside of components. Whether you have repetitive chunks of templates, or UI elements, or event entire parts of your app, you should consider using components.

Don't fear using components in components, the more "organic" your design / approach is, the more modular your components set will be. Oh, and you're likely to drink less coffee (think about your health Dude ^^)

Ember 2.0 will put even more emphasis on components!


### NOT THAT COOL points
- Before digging deeper in Ember, we have heard about its famous "learning curve". Some said it is like climbing a mountain, some compare it to a roller coaster. We tried and, we must admit, it's pretty heavy and almost sinusoidal, but really worth to surf. We've had bad days, and good days. We've had questions, we still have questions.
- Maybe the "convention over configuration" is not for everyone
- The way components communicate through actions is still very perfectible (notably the `sendAction()` method, which could be very confusing for beginners)


## Ember cli

### COOL points
+ The most cool point about Ember-cli is its EcmaScript6 transpiler! It's really cool to write imports without requirejs headhaches, and to be able to use ES6 features, right now.
+ It provides a full development environment with server, automatic incremental build with broccoli, live watch and reload, tests & jshint.
+ Ember cli is bundled with lots of cool generators following "blueprints" rules that allow you to keep up a good workflow
( create the right files, at the right place, create the corresponding basic tests,
  etc...) There is no way to make a mistake when using generators, which is a very gound point for scaling (product + team). Blueprints can be created, so every team can reproduce its own workflow
+ Ember-cli brings its own resolver that provides/allows a way better file architecture (PODs are also possible)
+ The current version (0.1.2) brought Content Security Policy, which is a cool addition if content security is important for your app, and the browsers you target are not yet compatible
+ Version 0.1.3 will let you create multiple sets of css files. To start with, we'll try ti use it to target specific needs (mobile, desktop, and why not old browsers). We can't wait for the upgrade (but after the beta has launched ^^)


### NOT THAT COOL points
- Despites Broccoli has really cool sides, the Brocfile is a bit complicated, and
  the "front" team is a little reserved, lack of documentation, too...
- Sass too long to be reloaded => NoCSS injection? (but it might change very soon => [see issue #2371 on ember-cli repo](https://github.com/stefanpenner/ember-cli/issues/2371))
- The upgrade process can be a real pain in the ass (this is a very very perfectible thing)

## Handlebars

### COOL points

- Handlebars is fully focused on templating, with just a bit of logic (making it very easy for HTML guys to use and understand). For more logic, use controllers
- Latest version made a great step towards more performance (those ugly metamorphs Dudes have disappeared) and version 2.0 (HTMLBars) promise to manipulate DOM elements vs strings (as with handlebars)


## Ember data

### COOL POINTS
  + Various adapters for various ways to use it (wanna use fixtures ? Use fixtureAdapter. Want to use firebase ? Download the firebase adapter, configure and run with a great smile, otherwise stay with the RESTAdapter)
  + Various methods to easily manage models and records
  + Records flags (isNew, isDirty, isSaving, etc....)

### NOT THAT COOL points
  Unleash the kraken!!
  - very opinionated. Too opinionated maybe? No option could be passed to `save()` etc..
  - pagination is still an issue for us
  - implements JSON API, but partially!
  - lot of monkey patching (if your API is not 100% ember-data compatible)
  - problems with socket.io, updating a model that is not already in collection?
  - other bullshit things?

  => plan in near future to throw it and re-implement something more modular like we have on Backbone?


## Internationalization

We tried [ember-i18n](https://github.com/jamesarosen/ember-i18n) that was a good start but did not embrace fully gettext philosophy. We had a look to [Jed](slexaxton.github.io/Jed/) and [i18nnext](http://i18next.com/) but there were both too complex, shipped too many unecessary features, so we came with our own plugin [LINK HERE] and [Handlebars xgettext parser](https://github.com/Wisembly/xgettext-php) written in PHP. We'll make in the near future a more complete post about internationalization and gettext / Poedit.


## Tests

We clearly did not had time to dig deeper the tests more than in the docs, we'll fill the gap once the beta open.


## Ember Inspector
A ~~very cool~~ mandatory chrome plugin to help you debug your ember.js app.

Review your views / routes structure, check the loaded data in the blink of an eye, analyze the rendering performance, found everything in your container, etc...


## The runLoop
Understand it will make your life easier (it can bring peace to the world too..)
[More explanations here](https://www.youtube.com/watch?v=G4DdNMLubgQ&feature=youtu.be)


## Conclusion ?
[Nico]
When we begun our POCs (angular.js VS ember.js), I was clearly an Angular guy... My personal tests, and let's admit it, all the hype around Angular were telling me to use and promote Angular.

This was before making a more professional POC with Angular and testing Ember.js a bit deeper!

I really felt in love with Ember.js and all its philosophy (this is not entirely because Tomster is sexy ^^), and enjoy it every day.

Very happy with it at the time we write this article, the future seams shiny too ;)
Ember.js 2.0 looks as a cool as the next StarWars trailer.
[Check the road to Ember.js 2.0](https://github.com/emberjs/rfcs/pull/15) and [the discussions about it](https://news.ycombinator.com/item?id=8551897) on HackerNews

Ember.js really smells like something more strong, complete and SOLID, which happens to be a perfect match for the apps we want to build now and in the future.
