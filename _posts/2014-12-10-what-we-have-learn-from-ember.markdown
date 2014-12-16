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

Here [@Wisembly](http://wisembly.com) we strive to change the way people meet, work and collaborate during meetings. We come from a Symfony2 / Backbone.js / socket.io world with our event / training / conf call products, and when it came to thinking about our next product, [Solid](http://getsolid.io), we slowed down things a bit and looked for a different and a better way to manage our frontend application.

We looked at [Angular.js](https://angularjs.org/) and [Ember.js](http://emberjs.com/) that were trending among cool kids out there and that looked both promizing for us to manage an ambitious javascript application with our growing developpers team (by the way, [we are hiring!](http://wisembly.com/jobs)).

After doing the famous [Todo MVC example](http://todomvc.com/) and some other POCs, we decided to go for Ember with [Ember-cli](http://www.ember-cli.com/).

Here is our humble 3 months real life Ember.js feedback for [Solid](http://getsolid.io), what we have learnt, what we think is cool, what is really uncool and what could be improved.


## Ember.js

### Convention over configuration

**First of all, Ember is not like Backbone. It's a strongly opinionated MVC framework.**

That means devs accepting to embrace Ember's philosophy will be rewarded by the framework after the learning curve, whereas more skeptical ones will keep on fighting against concepts they may consider odd and won't unlock the true framework potential. But hey, nothing new here, that's the same for every opinated framework in any language.

Using Ember conventions and components will allow you, once masterized, to scale only your business complexity part inside your app with your growing team, instead of handling framework complexity and improvement (rendering, syncing data for example).

We observed that, even in a short 3 months long period window, we took 2 sprints of 2 weeks to set up our application foundations with 2 javascript developers and then handled in the last 2 sprints more features with only one dev that we would ever do with our current Backbone production application. Integrating an authentication mechanism? There's an ember-cli plugin for that. Integrating Google analytics, in our app? There's an ember plugin for that too.

It **feels right** to see in this javascript world with Ember the same benefits we experience with Symfony2 for a long time now with bundles and plugins that perfectly fit, that are easy to install or to maintain, thanks to the framework rigor and conventions.


### What does that mean for your team and your productivity

**Good points**
- Your developpers will tend to produce more homogeneous code. That's a great thing for productivity, maintenance and scalability
- New team members will already know Ember and will understand your code faster, they'll only have to look to your business code, no need for them to read and learn a framework related mechanism you could have developped inside your own framework
- You won't have to maintain core parts of your code. Just keep your project Ember-up-to-date to benefit from the latest community features and improvements. Again, no time wasted in maintaining something a community could maintain for you.

**Risks**
- What happens if you integrate an Angular dev or a Backbone dev? Despite the fact that Ember and Angular differs in many ways, their root concepts are not that far, and the new "dev on the block" should feel at home within days (1-2 weeks max)
- You should consider understanding and using "the ember way" to do things, before trying to customize or monkey patch them => think about tests, future upgrades, and glitches you should introduce in the app because "Hell yeah, I like to customize ALL THE THINGS"


### The world is made of components

Do you embrace DRY methodology? Components are your new friends ;)

Ember.js allows you to wrap all of your repeated pieces of code inside components. Whether you have repetitive templates chunks, or UI elements, or event entire parts of your app, you should consider using them.
Don't fear using components in components, the more "organic" your design / approach is, the more modular your components would be.

Another cool aspect of using components as a front-end developer / UI developer is to list UI oriented ones in a styleguide and, in that way, help developers to test, see regressions and find which ones are available with their parameters.

Ember 2.0 will put even more emphasis on components!


### Not very cool points

Before digging deeper into Ember, we heard about its famous "learning curve". Some said it is like climbing a mountain, some compare it to a roller coaster. We tried and we must admit, it's pretty heavy and almost sinusoidal, but really worth to surf.

We've had bad days and good days. We've had questions and we still have questions...

The first of these questions is about [Ember Data](https://github.com/emberjs/data). It's an awesome library, no doubt about it: well documented, very active, and strong / stable enough for what we want to build.
But the fact is that our APIs are not fully compatible with it: not fully "JSON API" compliant, and not very modifiable, since they are shared accross our products. Since Ember Data is not very permissive, we've had some headaches. That's why we are wondering if we shall build our own data store/cache/api layer.

In some cases, we still wonder where is the best place to do things and how to do it.
For example, let's say you have to implement a global notification center for your app: we're still investigating and iterating to find the best way to do it... Even if a "service" is what sounds like to be the best idea, it is not as simple as it seem...

How does it interact with push events (we make a heavy use of [socket.io](http://socket.io/) ? How does it interact with the "bubbling" of Ember actions ? What if a component has to notify the app of its state ? What if you want your models to auto-notify the user when they are saved / errored ?
We implemented all of these behaviors but we are not very sure if we did it the right way, and trying to find better methods every day (ok, finally it's pretty normal for devs ^^)

Maybe the "convention over configuration" is not for everyone, and not perfect for every cases. It might be sometimes inevitable to patch or get around things for your business needs and Ember "rigidity" will be more a burden.

The way components communicate through actions is still very perfectible (notably the `sendAction()` method, which could be very confusing for beginners)


## Ember cli

### COOL points

The coolest point about Ember-cli is its EcmaScript6 transpiler, clearly. It's really cool to write imports without requirejs headhaches and to be able to use ES6 features, right now.

Besides, it provides a full development environment with server, automatic incremental build with Broccoli, live watch and reload, tests & jshint.

Ember cli is bundled with lots of cool generators following "blueprints" rules that allow you to keep up a good workflow (create the right files, at the right place, create the corresponding basic tests, etc...). There is no way to make a mistake when using generators, which is a very good point for scaling (product + team). Blueprints can be created, so every team can reproduce its own workflow

In addition, Ember-cli brings its own resolver that provides/allows a way better file architecture (PODs are also possible)

#### A gift in every new version!
The version we are using (0.1.2) brought "Content Security Policy", which is a cool addition if content security is important for your app, and the browsers you target are not yet compatible.

Version 0.1.3 will let you create multiple sets of CSS files. To start with, we'll try to use it to target specific needs (mobile, desktop, and why not old browsers). We can't wait for the upgrade (but after the beta has launched ^^)


### Not very cool points

Despite, Broccoli has really cool sides, the Brocfile is a bit complicated, and our frontend team is a little reserved. This lacks some documentation too...

In addition, Broccoli looks like to be quite slow and less flexible compared to Gulp: the fact that it recompiles everything, including JS even if you change only a line of CSS is not good at all.
Thus, CSS is too long to be live reloaded and there is no CSS injection (but it might change very soon => [see issue #2371 on ember-cli repo](https://github.com/stefanpenner/ember-cli/issues/2371))

To finish, the upgrade process can be a real P.I.A (this is a very very perfectible thing)


## Handlebars

### Cool points

Handlebars is fully focused on templating, with just a bit of logic (making it very easy for HTML guys to use and understand). For more logic, use controllers!
Latest version made a great step towards more performance (those ugly metamorphs Dudes have disappeared) and version 2.0 / HTMLBars promise to manipulate DOM elements vs strings (as with handlebars)


### Not very cool points

Logic is **very** limited here. Okay, right, 99% of the logic should be made inside controllers as we said above, but sometimes we lack some tools and logic features to handle presentation logic that have nothing to do inside our application code, our models nor our controllers. When we say that logic is limited it is even a `AND` or `OR` condition in a `if` statement that is not possible. In fact, controllers are currently more "presenters" than controllers because they embed both application logic and presentation logic.



## Ember Data

### COOL POINTS
Ember Data comes with various adapters for multiple usage ways (Want to use fixtures? Use fixtureAdapter. Want to use firebase? Download the firebase adapter, configure and run with a great smile, otherwise stay with the RESTAdapter)

It also comes with various methods to easily manage models and records

We particularly like records flags (isNew, isDirty, isSaving, etc....), it's a fantastic feature !

### Not very cool points

Ember Data is **very** opinionated (too opinionated?). No option could be passed to `save()` and other methods, virtually impossible to extend.

For instance, pagination is still an issue for us today (hopefully we didn't have to deal with it at the moment)

Ember Data follows and implements JSON API standard, but partially! So we had to do a lot of monkey patching (will apply to you if your API is not 100% ember-data compatible)

We also had problems with socket.io, we still have questions like "updating a model that is not already in collection?""

We'd really like to have some time soon to look to that more deeply and consider not using ember data and find / create a data layer more modulable.


## Internationalization

We tried [ember-i18n](https://github.com/jamesarosen/ember-i18n) that was a good start but did not embrace fully gettext philosophy. We had a look to [Jed](slexaxton.github.io/Jed/), [i18nnext](http://i18next.com/) or [format.js](http://formatjs.io/) but there were too complex, shipped too many unecessary features, or did not follow gettext standards. So we came with our own tiny plugin [ember-gettext](https://github.com/Wisembly/ember-gettext). We'll make in the near future a more complete post about internationalization and gettext / Poedit standards and phylosophy.


## Tests

We clearly did not had time to dig deeper the tests more than in the docs, we'll fill the gap once the beta opens.


## Ember Inspector
A ~~very cool~~ mandatory chrome plugin to help you debug your ember.js app.

Review your views / routes structure, check the loaded data in the blink of an eye, analyze the rendering performance, find everything in your container, etc...


## The runLoop
Understand it will make your life easier (it can bring peace to the world too..)
[More explanations here](https://www.youtube.com/watch?v=G4DdNMLubgQ&feature=youtu.be)


## Conclusion ?

When we begun our POCs (angular.js VS ember.js), all the hype around Angular were telling us to use it. We really liked Ember.js and its philosophy. It was more "us", coming from backend for some of us from Symfony or RoR. We liked the robustness of Ember in the shadow of Angular fame and glory.

We are very happy with it at the time we write this article, and the future seams quite bright to, Ember.js 2.0 looks as cool as the next StarWars trailer.
[Check the road to Ember.js 2.0](https://github.com/emberjs/rfcs/pull/15) and [the discussions about it](https://news.ycombinator.com/item?id=8551897) on HackerNews.

Ember.js really feels like something strong, complete and SOLID, which happens to be a perfect match for the apps we want to build now and in the near future.


If you liked this blog post, please register to our [solid beta and next week challenge us on our application](http://getsolid.io), and thanks to the Ember console inspector help us improve and challenge us. And maybe during this process, our product will help you organize even better scrum meetings!
