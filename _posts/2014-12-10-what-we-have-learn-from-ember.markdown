---
layout:     post
title:      "What we've learn from Ember.js after 2 months developing our new product. A Solid story"
categories:
  - general
  - ember
  - javascript
  - front
  - backend
author:     guillaumepotier
---

Here [@Wisembly](http://wisembly.com) we strive to change the way people meet, work and collaborate during meetings. We come from a Symfony2 / Backbone.js / socket.io world with our event / training / conf call products, and when it came to thinking about our next product, [Solid](http://getsolid.io), we slowed down things a bit and looked for maybe a different and possibly better way to manage our frontend application.

We looked at [Angular.js](https://angularjs.org/) and [Ember.js](http://emberjs.com/) that were trending among cool kids out there and that looked both promizing for us to manage an ambitious javascript application with our growing developpers team (by the way, [we are hiring!](http://wisembly.com/jobs)).

After doing the famous [Todo MVC example](http://todomvc.com/) and some other POCs, we decided to go for Ember with [Ember-cli](http://www.ember-cli.com/).

Here is ou humble 3 months real life Ember.js feedback for [Solid](http://getsolid.io), what we learnt, what we think that's cool, what is really uncool and what could be improved.


## Ember.js

### Convention over configuration

**First of all, Ember is not like Backbone. It's not a library, it's a framework.**

That mean devs accepting to embrace Ember's philosophy will be rewarded by the framework after the learning curve, whereas more sckeptical ones will keep fighting against concepts they may consider odd and won't unlock the framework potential. But hey, nothing new here, that's the same for every opinated framework in any language.

Using Ember conventions and components will allow you, once masterized, to scale only your business complexity part inside your app with your growing team, instead of handling framework complexity and improvement (rendering, syncing data for example).

We observed that, even in a short 3 months long period window, we took 2 sprints of 2 weeks to set up our application foundations with 2 javascript developers and then handled in the last 2 sprints more features with only one dev that we would ever do in our current Backbone production application. Integrating an authentication mechanism? There's an ember-cli plugin for that. Integrating Google analytics, Intercom or Mixpanel in our app? There are ember plugins for that too.

It **feels right** to see in this javascript world with Ember the same benefits we experience with Symfony2 for long now with bundles and plugins that perfectly fit, easy to install or to maintain, thanks to the framework conventions.


### What does that mean for your team and your productivity

**Good points**
- Your developpers will tend to produce more homogeneous code. That's a great thing for productivity, maintenance and scalability
- New team members will already know Ember and will understand your code faster, they'll only have to look to your business code, no need for them to read and learn a framework related mechanism you could have developped inside your own framework
- You won't have to maintain core parts of your code. Just keep your project Ember-up-to-date to benefits for latest community features and improvements. Again, no more team time waster to maintain something a community could maintain for you

**Risks**
- What happens if you integrate an "Angular" dev? Despite the fact that Ember and Angular differs in many ways, their root concepts are not that far, and the new "dev on the block" should feel at home within days (1-2 weeks max)
- You should consider understanding and using "the ember way" to do things, before trying to customize them => think about tests, future upgrades, and glitches you should introduce in the app because "Hell yeah, i like to customize ALL THE THINGS"

### The world is made of components

Do you embrace DRY methodology? Components are your new little friends ;)

Ember.js allows you to wrap all of your repeated pieces of code inside components. Whether you have repetitive chunks of templates, or UI elements, or event entire parts of your app, you should consider using them.

Don't fear using components in components, the more "organic" your design / approach is, the more modular your components will be. Oh, and you're likely to drink less coffee (think about your health Dude ^^)

Ember 2.0 will put even more emphasis on components!


### NOT THAT COOL points
- Before digging deeper into Ember, we heard about its famous "learning curve". Some said it is like climbing a mountain, some compare it to a roller coaster. We tried and, we must admit, it's pretty heavy and almost sinusoidal, but really worth to surf. We've had bad days, and good days. We've had questions, and we still have questions.
- Maybe the "convention over configuration" is not for everyone
- The way components communicate through actions is still very perfectible (notably the `sendAction()` method, which could be very confusing for beginners)


## Ember cli

### COOL points
+ The coolest point about Ember-cli is its EcmaScript6 transpiler, clearly. It's really cool to write imports without requirejs headhaches, and to be able to use ES6 features, right now.
+ It provides a full development environment with server, automatic incremental build with Broccoli, live watch and reload, tests & jshint.
+ Ember cli is bundled with lots of cool generators following "blueprints" rules that allow you to keep up a good workflow (create the right files, at the right place, create the corresponding basic tests, etc...) There is no way to make a mistake when using generators, which is a very good point for scaling (product + team). Blueprints can be created, so every team can reproduce its own workflow
+ Ember-cli brings its own resolver that provides/allows a way better file architecture (PODs are also possible)
+ The current version (0.1.2) brought Content Security Policy, which is a cool addition if content security is important for your app, and the browsers you target are not yet compatible
+ Version 0.1.3 will let you create multiple sets of css files. To start with, we'll try ti use it to target specific needs (mobile, desktop, and why not old browsers). We can't wait for the upgrade (but after the beta has launched ^^)


### NOT THAT COOL points
- Despites Broccoli has really cool sides, the Brocfile is a bit complicated, and our frontend team is a little reserved. This lacks some documentation too...
- Sass is too long to be reloaded => NoCSS injection? (but it might change very soon => [see issue #2371 on ember-cli repo](https://github.com/stefanpenner/ember-cli/issues/2371))
- The upgrade process can be a real P.I.A (this is a very very perfectible thing)


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

We tried [ember-i18n](https://github.com/jamesarosen/ember-i18n) that was a good start but did not embrace fully gettext philosophy. We had a look to [Jed](slexaxton.github.io/Jed/) and [i18nnext](http://i18next.com/) or [format.js](http://formatjs.io/) but there were too complex, shipped too many unecessary features, or did not follow gettext standards, so we came with our own tiny plugin [ember-gettext](https://github.com/Wisembly/ember-gettext). We'll make in the near future a more complete post about internationalization and gettext / Poedit standards and phylosophy.


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
