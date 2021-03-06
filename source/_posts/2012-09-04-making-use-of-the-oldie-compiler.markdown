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

This approach worked and all in all was fine. However, like most developers I became lazy. I got tired of copying styles I had written in media queries and pasting them where I could scope them with an ```.oldie``` class. Even when I was writing my styles in Less it was still a burden to copy my styles in both my 768 and 960 breakpoints and paste them in the scope of my ```.oldie``` class. It was evident I needed another solution.

##The Lightbulb Moment

After several over-complicated attempts I realized re-inventing the wheel wasn't needed. Since I was already writing my styles with a CSS compiler such as Less or Sass all I had to do was harness the power of the mixins. 

_Cue the mother-fucking lightbulb!_

<!-- more -->

All I had to do was write my breakpoint specific styling in several mixins and then I could import them in the ```.oldie``` class and specified media queries at the bottom of the page. The solution was so simple I wanted to kick myself in the face.

##The Implimentation

For those not familiar with CSS compilers such as Less or Sass, mixins allow a block of styles to be reused throughout an application simply by scoping them inside a named class or include. This makes it possible to re-purpose whole chunks of styling and thus avoid repeating yourself throughout the application. In this case this was exactly the thing I needed to recreate my ```.oldie``` class.

To do this in Sass I simply just created two breakpoint mixins like so:

<figure class='code'><figcaption><span>Breakpoint Mixins </span></figcaption>
 <div class='highlight'><table><tbody><tr><td class='gutter'><pre class='line-numbers'><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
<span class='line-number'>4</span>
<span class='line-number'>5</span>
<span class='line-number'>6</span>
<span class='line-number'>7</span>
</pre></td><td class='code'><pre><code class='SASS'><span class='line'> <span class='c1'>//all global and mobile-specific styling</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@mixin</span><span class='nf'> sevensixtyeight</span>
</span><span class='line'>      <span class='c1'>//all min-width:768px styles go here</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@mixin</span> <span class='nc'>ninesixty</span>
</span><span class='line'>      <span class='c1'>//all min-width:960px styles go here</span>
</span></code></pre></td></tr></tbody></table></div></figure>

Instead of placing my styles in a media query like so: ```@media (min-width:x) { ... }``` I could place all my breakpointed styles into the mixins I had created above which would be rendered into the stylesheet when and where I needed. Simple.

Next I created my actual compiler where I would import the mixins at the needed breakpoints and repurpose them within the scope of my ```.oldie``` class.

<figure class='code'><figcaption><span>Simple Oldie Compiler </span></figcaption>
 <div class='highlight'><table><tbody><tr><td class='gutter'><pre class='line-numbers'><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
<span class='line-number'>4</span>
<span class='line-number'>5</span>
<span class='line-number'>6</span>
<span class='line-number'>7</span>
<span class='line-number'>8</span>
<span class='line-number'>9</span>
<span class='line-number'>10</span>
<span class='line-number'>11</span>
<span class='line-number'>12</span>
</pre></td><td class='code'><pre><code class='SASS'><span class='line'> <span class='c1'>//Compiler</span>
</span><span class='line'>  <span class='c1'>//No breakpoint specific styles here</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span><span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:768px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> sevensixtyeight</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span><span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:960px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> ninesixty</span>
</span><span class='line'>
</span><span class='line'>  <span class='nc'>.oldie</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> sevensixtyeight</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> ninesixty</span>
</span></code></pre></td></tr></tbody></table></div></figure>

BOOM! I was done. Everything I wrote in my ```.sevensixtyeight()``` and ```.ninesixty()``` mixins could be imported simultaneously into my ```.oldie``` class with ease. 

##Extending this capability

I was very content with this functionality. So much so that my colleages and I began using this model immediately without really discussing the ways in which we planned to extend the functionality. I mean why would we? All of our current problems had been solved.

A few weeks ago <a href='https://twitter.com/gesa' title='@gesa'>@gesa</a> shared a gist with me of how she had included HD, retina, and mobile-specific media queries into her oldie compiler. Stupid simple. Again I wanted to kick myself in the face that I hadn't thought of this myself. The solution was simple just add the following optional mixins: ```.foureighty()```, ```.tweleveeighty()```, ```.nineteentwenty()```, ```.retina()``` in Less and ```@include foureighty```, ```@include tweleveeighty```, ```@include nineteentwenty```, ```@include retina``` in Sass.

<figure class='code'><figcaption><span>Extended Oldie Compiler </span></figcaption>
 <div class='highlight'><table><tbody><tr><td class='gutter'><pre class='line-numbers'><span class='line-number'>1</span>
<span class='line-number'>2</span>
<span class='line-number'>3</span>
<span class='line-number'>4</span>
<span class='line-number'>5</span>
<span class='line-number'>6</span>
<span class='line-number'>7</span>
<span class='line-number'>8</span>
<span class='line-number'>9</span>
<span class='line-number'>10</span>
<span class='line-number'>11</span>
<span class='line-number'>12</span>
<span class='line-number'>13</span>
<span class='line-number'>14</span>
<span class='line-number'>15</span>
<span class='line-number'>16</span>
<span class='line-number'>17</span>
<span class='line-number'>18</span>
<span class='line-number'>19</span>
<span class='line-number'>20</span>
<span class='line-number'>21</span>
<span class='line-number'>22</span>
<span class='line-number'>23</span>
<span class='line-number'>24</span>
</pre></td><td class='code'><pre><code class='SASS'><span class='line'> <span class='c1'>//Compiler</span>
</span><span class='line'>  <span class='c1'>//No breakpoint specific styles here</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span> <span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:480px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> foureighty</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span><span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:768px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> sevensixtyeight</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span><span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:960px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> ninesixty</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span><span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:1280px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> tweleveeighty</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span><span class='o'>(</span><span class='nt'>min-width</span><span class='nd'>:1920px</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> nineteentwenty</span>
</span><span class='line'>
</span><span class='line'>  <span class='k'>@media</span> <span class='o'>(</span><span class='nt'>-webkit-min-device-pixel-ratio</span> <span class='nd'>:</span> <span class='nt'>1</span><span class='nc'>.5</span><span class='o'>),(</span><span class='nt'>min-device-pixel-ratio</span> <span class='nd'>:</span> <span class='nt'>1</span><span class='nc'>.5</span><span class='o'>)</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> retina</span>
</span><span class='line'>
</span><span class='line'>  <span class='nc'>.oldie</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> sevensixtyeight</span>
</span><span class='line'>      <span class='k'>@include</span><span class='nd'> ninesixty</span>
</span></code></pre></td></tr></tbody></table></div></figure>

None of these new media queries are required since by default since none of these mixins are necessarily needed in the ```.oldie``` class. However, it's good to have them included just in case you may need to re-purpose them later in your application. 

##Pros & Cons

###Pros:

* Saves time by compiling any needed media queries into an oldie specific classes
* Can be re-purposed cross-application

###Cons: 

* None really other then the fact you'll need to install either Sass or Less as well as Node and any other dependencies.

## Final Thoughts

One last thought. The other day I was reading a <a href='http://simurai.com/post/30451824480/media-query-splitting' title='great post'>great post</a> regarding 'media query splitting' written by <a href='https://twitter.com/simurai' title='@simurai'>@simurai</a>. I rather liked this  organizational approach other then the fact that it didn't work for ```.oldie``` specific styling. The Oldie Compiler model solves this issue and makes this a very viable option. 

## More Info

<a href='https://github.com/seawolff/oldiecompiler' title='Check out Oldie Compiler on Github'>Check out Oldie Compiler on Github</a> 
