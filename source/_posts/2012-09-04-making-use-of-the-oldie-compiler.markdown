---
layout: post
title: "Making use of the Oldie Compiler"
date: 2012-09-04 12:53
comments: yes
categories: ['HTML5 Boilerplate', CSS', 'Less', 'Sass']
---

##The Joy of CSS Conditional Comments

Undoubtably the most masterful thing about Paul Irish's HTML5 Boilerplate is the IE CSS conditional comments to be found at the beginning of the boilerplate itself. CSS conditional comments, such as the oldie conditional found in the Boiler Plate, allow the developer to use page-specific javascript and styles which play a huge role in developing HTML5 applications. 

##The Problem

Now typically the more I write mobile-first, breakpoint-specific styling the more I have to repeat myself. It's simply a given. Most UI Engineers will take the approach of working top down, organizing all their styles from the global scope to mobile, to tablet, to desktop to HD, etc. This is all fine and dandy until you get to styling for your 'oldie' IE browsers [IE 6/7/8] which don't support media queries. 

Previously my thought process to solving this was the following: 
	
_"Simple! I'll just copy all my styles in my breakpoints and paste them seperately by prepending an .oldie class to the selectors."_

This approach worked and all in all was fine. However, like most developers I became lazy. I got tired of having to copy new styles I had written in a media query and pasting them where I could scope them with an ```.oldie``` class. Even when I was writing my styles in Less it was still a burden to copy my styles in both my 768 and 960 breakpoints and paste them in the scope of my ```.oldie``` class. It was evident I needed another solution.

##The Lightbulb Moment

After several over-complicated attempts I realized re-inventing the wheel wasn't needed. Since I was already writing my styles with a CSS compiler such as Less and Sass all I had to do was harness the power of the mixins. 

_Cue the mother-fucking lightbulb!_

All I had to do was write my breakpoint specific styling in several mixins and then I could import them in the ```.oldie``` class and specified media queries at the bottom of the page. The solution was so simple I wanted to kick myself in the face.

##The Implimentation

For those not familiar with CSS compilers such as Less or Sass mixins allow a block of styles to be reused throughout an application simply by scoping them inside a named class or include. This makes it possible to re-purpose whole chunks of code and thus avoid repeating styling throughout the application, which in this case was exactly the thing I wanted to use to recreate my ```.oldie``` class.

To do this in Less I simply just created two breakpoint mixins like so:

	//all global and mobile-specific styling

	.sevensixtyeight() {
		//all min-width:768px styles go here
	}

	.ninesixty() {
		//all min-width:960px styles go here
	}

Instead of placing my styles in a media query like so: ```@media (min-width:x) { ... }``` I could place all my breakpointed styles into the mixins I had created above which would only be rendered into the stylesheet when and where I needed. Simple.

Next I created my actual compiler where I would import the mixins at the needed breakpoints and repurpose them within the scope of my ```.oldie``` class.

	@media(min-width:768px) {
		.sevensixtyeight();
	} @media(min-width:960px) {
		.ninesixty();
	} .oldie {
		.sevensixtyeight();
		.ninesixty();
	}

BOOM! I was done. Everything I wrote in my ```.sevensixtyeight()``` and ```.ninesixty()``` mixins could be imported simultaneously into my ```.oldie``` class with ease. 

##Extending this capability

I was very content with this functionality. So much so that my colleages and I began using this model immediately without really discussing the ways in which we planned to extend the functionality. I mean why would we? All of our current problems had been solved.

A few weeks ago <a href='https://twitter.com/gesa' title='@gesa'>@gesa</a> shared a gist with me of how she had included HD, retina, and mobile-specific media queries into her oldie compiler. Stupid simple. Again I wanted to kick myself in the face that I hadn't thought of this myself. The solution was simple just add the following optional media queries: 

	@import (min-width:480px) {
		.foureighty();
	} @media(min-width:1280px) {
		.tweleveeighty();
	} @media(min-width:1920px) {
		.nineteentwenty();
	} @media (-webkit-min-device-pixel-ratio : 1.5),
	(min-device-pixel-ratio : 1.5) {
		.retina();
	}

None of these new media queries need to be required since by default none of these mixins are necessarily needed in the ```.oldie``` class. However, it's good to have them included just in case you may need to re-purpose them later in your application. 

##Pros & Cons

###Pros:

* Saves time by compiling any needed media queries into an oldie specific classes
* Can be re-purposed cross-application

###Cons: 

* None really. You'll need either CSS or Less installed as well as any other dependencies. But other then that you're golden.

## Final Thoughts

One last thought. The other day I was reading a <a href='http://simurai.com/post/30451824480/media-query-splitting' title='great article'>great article</a> regarding 'media query splitting' written by <a href='https://twitter.com/simurai' title='@simurai'>@simurai</a>. I rather liked this approach to organization other then the fact that it didn't work for ```.oldie``` specific styling. The Oldie Compiler model solves this issue and makes this a very viable option. 

## More Info

<a href='https://github.com/seawolff/oldiecompiler' title='Check out Oldie Compiler on Github'>Check out Oldie Compiler on Github</a> 
