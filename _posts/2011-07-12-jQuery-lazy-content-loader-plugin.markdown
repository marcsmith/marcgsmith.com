--- 
layout: post
title: "jQuery lazy content loader plugin"
---
## Why did i do this?
While it's debatable that the site i work on for my day job suffers from "content overload" on its homepage (i won't tell you which side of the debate i'm on), the developers have been fortunate enough to get some time to work on site performance.  It's a shame that this isn't a top priority all of the time, but i digress...

Anyhow, one thing we've pinpointed is that we have a great deal of content that's not visible on the initial page paint - things in carousels, tabbed/accordion areas, etc.
Our homepage is large.  Way large.  197K last i checked.  HFS, yeah....that's what i said.

So i got to thinking...what if we load only what's visible (to oversimplify), and load everything else "on demand" based on user actions or time?  (sure, novel idea 10 years ago...don't judge)

<!-- After doing the usual searching around for a nice (jQuery preferred) plugin to help out, i found that for what i wanted i couldn't find something robust/flexible enough.  So here's what i came up with to meet our needs, and hopefully yours. -->

## Ok, what assumptions do i need to make about the markup in my page?

Two things, really.
1. This relates to the markup used for the content items, and the controls used to grab the external content to fill those items.  Both the content and controls are each structured as unordered lists (&lt;ul&gt;), and each item in the content list has a corresponding item in the control list.  Reasonable.
2. Each of your control elements will have a jQuery data key/value attached to it, which specifies the URL where the content for that control item lives. OR, if you don't want a URL attached to every single control item (and thus, need to make an ajax call for each item), you can bind a single data value to the &lt;ul&gt; of the controls and just one fetch will be made (presumably) for ALL of your data.  See demos for examples.

## How will it work?
At its simplest, this will lazily load content (html, json, etc), based on a custom event that you specify - eg., a click, hover, whatever - you choose.
The only other thing you'll need to specify is a callback function that will be called once your content is successfully fetched (error handling/callback not finished yet).
Your external data (and more, keep reading) is sent to your callback, and you can go nuts filling DOM elements with your goodies.

There are a few options that make this super flexible, so let's check them out.

#DEMOS:

##Click (trigger) tabs in a tabbed content area
Just like it sounds - get content when user clicks a tab. Click for demo:
<img src="./projects/lazyContentLoader/demo/images/demo_tabs.png" class="group demo" />

##Click (trigger) a spot in a content carousel
Similar to the first example, but the callback here get a little fancier by sliding the carousel left or right. Click for demo:
<img src="./projects/lazyContentLoader/demo/images/demo_caro.png" class="group demo" />

##Mouseenter (trigger) on site navigation elements, with 2nd trigger (mouseleave) & callback for clearing content action
So, we get a little fancier here. The user directs mouse over our control element and content is fetched.  Then, when the second trigger is invoked, the content area gets cleared by way of a second callback.  You could use that second trigger for anything, i presume (not necessarily for clearing/hiding the fetched content).
The great thing here is that
<img src="./projects/lazyContentLoader/demo/images/demo_nav.png" class="group demo" />

