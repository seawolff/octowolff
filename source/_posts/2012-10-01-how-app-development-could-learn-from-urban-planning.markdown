---
layout: post
title: "How web development could take a lesson from urban planning"
date: 2012-10-02 16:20
comments: true
categories: 
---

Over half of the world's population lives in urban areas - a number that is expected to grow to about 75% by the year 2050. This fact is becoming exponentially clear to urban planners, architects, builders, and designers the world over. But what does this mean? It means that in the next 35 years we as humans will have to reshape the way we live and work together.

As a web developer I was quick to draw a correlation between urbanization and the current state of the web. A few years ago it was assumed that the average user was comfortable, stationary, and had a high speed connection. However now we live in a world where just about every device has the ability to connect to the Internet. We no longer can dictate how our users consume our content. And in that vein it has become extremely important for those of us working in the web to understand the ubiquity of our content. 

In this way we as web designers and developers are facing the daunting role of adapting to how humans interact with our content. A role not too different from urban planners and designers facing rapid urbanization. 

<!-- more -->

##Embrace Unpredictability

I recently attended a talk at [Web Visions conf](http://www.webvisionsevent.com/chicago/) in Chicago by [Brad Frost](https://twitter.com/brad_frost) In which he talked about the need to create a future friendly web experience. He addressed the fact the current web standards we have in place just simply won't hold up to the number of devices that are being created to connect to the web. The solution he proposed is to embrace unpredictability. Just as city planners and developers can't dictate how its residents live, we as web developers and designers can't dictate how our users interact with our content.

##So where does that leave us? 

Well if you're like me you're an insufferable optimist. And while its easy to get mad that some kid is potentially trying to access one of my applications via his shitty game console and thus getting a shitty user experience, I think the appropriate response is instead one of acceptance and joy. It's important for us to embrace this diversity. 

##We're human after all right? 

Naturally my first reaction to the kid trying to access my app via his shitty game console or his mother trying to view it on her ancient blackberry device is "You're doing it wrong!" I mean after all if you have a shitty web browser you deserve a shitty user experience right?

It's easy for us to assume that our users should have the latest mobile webkit browser and be on an LTE connection. But the truth is we'd be wrong. In the same way that we'd be wrong to assume that all users have a car and a means of driving it to work or wherever they need to go. We can assume nothing.

##Paying attention to content

It's so easy for developers to assume. Just as we'd be wrong to assume that all of our users have a car, we'd be wrong to assume that our users want a separate mobile site or adversely a user experience with all the same features and navigation as the desktop users. This is why it's important to pay attention to content strategy. 

Problems happen. For example: traffic and large cities go hand in hand. When large groups of individuals are trying to get from point a to point b simultaneously you're bound to find yourself in a traffic jam. The same can be said in the web world. It's important for us to be flexible in how we solve the issue of user interaction. For instance, if a majority of your users are accessing your application on a sub-par data connection, it could be assumed that even the most advanced responsive site will move at the rate of bumper to bumper traffic. This is why it's important to audit content first before focusing on how you develop your mobile application. This way you won't simply be forcing all your devices in the metaphorical bike lane unless the context is appropriate. 

##Traffic? So why not just build a fucking highway?

Excusing the crude metaphor: assume our highway in this instance represents the approach of graceful degradation. If we build on a flexible grid then our desktop layout can break down to mobile. Boom. We're getting our content to smaller devices and our clients are happy. Done! The only issue with this is we're still left with extraneous elements that may not work on mobile.  **A.K.A. We're still stuck in traffic.** Mobile-first development allows the designer or developer to focus on the important UI elements and cut out extraneous distractions.

Again allow me to take the adverse viewpoint. We cannot just create a responsive, mobile-first experience via media queries and be done with it. As Brad pointed out in his talk, responsive web design is simply just the tip of the iceberg. Issues such as content strategy, performance, ergonomics, touch, feature detection, and conditional loading are just a few of the important issues that make up true progressive enhancement. 

##Let your content be freeeeee!

Your content should move with you. I've always had a deep hatred for share buttons and bookmarks. I hate using them because it's simply a marker pointing to where the origin of the content lives instead of bringing my content where I want it. Your content should revolve around your users. In that way it's important to allow it to be partitioned so it can be ported to a container of any size.

Copenhagen, Denmark took a very interesting approach to solving their transportation problems. They separated their bike lane from the road by a lane of parked cars. This encouraged bikers who were nervous about biking in the street to feel more comfortable about biking to and from where they need to go. Consider this to be our content extraction layer. It's important to have this separation between content and display. Your interface should consist of coordinated templating that pulls content from its base into whatever display is appropriate. This way you only need to write your content once in CMS while still re-purposing it as many times as needed. 

##Change we can believe in

_Cue obligatory Obama 08 poster_

Keep your chin up. It's so easy to feel bogged down by the rapid progression of the web. Especially if you have an eye to standards. This is an exciting time to work with the web or even to live in the world. Change is good. And frankly we're gonna' have a lot of it in our lifetime both on the web and off.

The important factor is to keep future friendly thinking. Focus on multiple access points for your content, and make sure to keep your design mobile-accessible first and foremost. Most importantly don't run away from the fact that your application will look like shit on your neighbor's high-tech Internet-accessible refrigerator thing-a-mabob. Embrace it. And if it's valuable to your users and business over the long-term it will pay off in the future.

###Sources:

* [Brad Frost WebVisions talk]( http://blog.manikrathee.com/posts/2012/09/28/brad-frost-future-friendly-web.html)
* [futurefriend.ly](http://futurefriend.ly)
* [Content First](http://adactio.com/journal/4523/)
* [Mobile First](http://www.lukew.com/ff/entry.asp?933)
* [Orbital Content](http://www.alistapart.com/articles/orbital-content/)

