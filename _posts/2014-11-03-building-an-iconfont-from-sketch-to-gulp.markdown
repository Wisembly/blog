---
layout:     post
title:      "Building an iconfont from Sketch to Gulp"
thumbnail:  "/public/images/font.jpg"
categories:
  - frontend
author:     gabrielcousin
---

~~In September, Wisembly started the development of a new product, which will transform your small meetings. Teasing!~~
**After several months of private beta testing and improvements, you are now free to use [Solid](http://getsolid.io).**

To do so, the dev team chose to use various frameworks and task runner such as Ember, Broccoli and Gulp.

In the front-end development of our 'older' app and for now, we used Grunt. But we saw that Gulp offers a lot of benefits: it is way faster and multitask. We decided to give it a try and took the occasion to make both workflows uniform.

### Less talk, more action!
CSS optimization will be detailed in a further post. This post is about building a homemade iconfont with Sketch and Gulp.

~~[By the way, you can fork this project on GitHub.](https://github.com/Wisembly/wisemblyiconfont)~~

**This repo is no more maintained. We use the same *but updated* workflow on our CSS framework [Tapestry](http://github.com/Wisembly/tapestry)**

We had some constraints like supporting IE7/8. It means that you have to build SVG, WOFF and… EOT. You will notice the original task is building SVG, WOFF, TTF and EOT:

1. [SVG fonts](http://caniuse.com/#feat=svg-fonts) are only supported by Safari and Android browsers.
2. [WOFF](http://caniuse.com/#feat=woff) is well supported (excepted IE8)
3. [EOT](http://caniuse.com/#feat=eot) is supported by all IE.
4. For the record: WOFF2 is coming soon with a great compression feature (about 30% more than WOFF), but is [not really well supported](http://caniuse.com/#feat=woff2) on recent browsers.

… so, you may cover a wide range of users with WOFF and EOT. That is why we decided not to import SVG and TTF into our CSS files.


Until we discovered [Sketchtool](http://bohemiancoding.com/sketch/tool/), we had to manually export each icon in SVG. Now, the Gulp task is directly using your Sketchfile.

Also, with Sketch 3.1, file type and extension were reviewed. Sketchfiles are no more a kind of zip file, so you can use it even more easily on GitHub.

### File structure
Tidy your bedroom, prepare your files and sort them, as done in this example:

	| dist *
	|- css *
	|- font *
	|- svg *
	| src
	|- sketch
	|- templates

(*) these folders will be created by Gulp.

### Plugins
For our spectific task, we will used the following plugins:

* [gulp-sketch](https://github.com/cognitom/gulp-sketch)
* [gulp-iconfont](https://github.com/nfroidure/gulp-iconfont)
* [gulp-consolidate](https://github.com/timrwood/gulp-consolidate)
* lodash

You need to have Sketch and Sketchtool installed.

__Before you launch the task : get your Sketchfile ready by flattening your icons and be sure you have one artboard per icon.__

### Script

	gulp.task('icons', function(){

	  return gulp.src('src/sketch/icons.sketch')

	  // extracting SVG from Sketchfile
	  .pipe(sketch({
	    export: 'slices',
	    formats: 'svg',
	    compact: 'yes',
	    saveForWeb: 'yes'
	  }))
	  .pipe(gulp.dest('dist/svg/'))

	  // creating SVG, TTF, WOFF, EOT
	  .pipe(iconfont({
	    fontName: 'icons',
	    appendCodepoints: false,
	    normalize: true,
	    centerHorizontally: true,
	    fontHeight: 100 // IMPORTANT
	  }))

	  // creating CSS files and sample page
	  .on('codepoints', function(codepoints, options) {

	    // options
	    var iconsOptions = {
	      glyphs: codepoints,
	      fontName: 'WisemblyIconfont',
	      fontPath: '../font/',
	      className: 'icon',
	    }

	    // template for modern browsers
	    gulp.src('src/templates/icon-template.css')
	    .pipe(consolidate('lodash', iconsOptions))
	    .pipe(rename('icons.css'))
	    .pipe(gulp.dest('dist/css/'));

	    // template for IE
	    gulp.src('src/templates/icon-template-ie.css')
	    .pipe(consolidate('lodash', iconsOptions))
	    .pipe(rename('icons-ie.css'))
	    .pipe(gulp.dest('dist/css/'));

	    // creating a sample page
	    gulp.src('src/templates/icon-template.html')
	    .pipe(consolidate('lodash', iconsOptions))
	    .pipe(rename({ basename:'sample' }))
	    .pipe(gulp.dest('dist/'));

	  })
	  .pipe(gulp.dest('dist/font/'));

	});
