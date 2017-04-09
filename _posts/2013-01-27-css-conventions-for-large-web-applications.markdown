---
layout: post
title: CSS Conventions for Large Web Applications
date: '2013-01-27 17:00:00'
author: Mark Host
---

The quality of CSS in large teams can get over-looked and as long as things look right, no one seems to notice.  Over the years I've been guilty of poorly structured stylesheets and had to pay for it in wasted time.  I've developed a set of preferences over time, mostly stolen from [modern](http://css-tricks.com/) [web](http://snook.ca/) [legends](http://meyerweb.com/).  

Here is the gist: 

* Use ID's for Javascript targeting and class's for CSS selectors
* Camelcase ID's and hypenate classes
* Understand and implement a modular architecture for your styles 
* Use a CSS preprocessor

The first two items are mostly for increased readabilty, but all of these tips will save you time now and leave your team with more maintable stylesheets.
____


### ID for Javascript &mdash; Class for Styles  

If possible, keep DOM selection for ID's and only use classes when targeting multiple elements at once. The difference in Javascript selector performance is minute and only noticeable when you have a large amount of DOM traversing, but ID's are technically faster.  It may not be noticeable, but it's a good rule to follow.

Using class-based selectors for styles makes life easier.  I've had predicaments in which styles were applied to ID's using by Javascript, embedded stylesheets or an external stylesheet.  This caused issues with the cascading hierarchy and the intended styles needed a beefed up hierarchy.  You can override this using <code>!important</code>, but that's sloppy and unmaintable.  If you need to add ID's to raise the hierarchy, that style now becomes dependent on a particular HTML structure. 

Stick to using classes for your style and you won't cause anyone issues now or later.   


### Format CSS Selectors Similar to Their Usage

If we use ID's for Javascript then we should style them like our Javascript code.  A programmers preference is to camelcase for readability.  Within the HTML/CSS it also helps understand what the selectors are being used for.  It immediately indicates behavior is attached to that element.  

The naming pattern assists reading similar to global variables in all-caps, functions being capitalized and variables camelcased. The formatting gives deeper meaning aside from the name itself, making the HTML/CSS more maintable and readable.


### Once You Preprocess, You'll Never Go Back

There once was a time when I wrote all my CSS by hand.  Those days are over.

If you're lucky to have middleware perform the preprocessing, you're in a good place. If not, you should compile your styles on your local machine before deploying, it's worth setting up your workflow to include a preprocessor.

The benefits are immediate after setup and a quick documentation read.  You write less code.  It's easier to read and maintain, therefore making changes much easier.  Somewhere along the line your styles become smarter.  Leading me to my next point.



### Everybody's Doing It, Or Atleast You Should Be Too

Jonathon Snooks' [SMACSS](http://smacss.com/) is the authority on the subject and this structure is gaining popularity; Twitter Bootstrap uses it and some big sites such as Yahoo employ this technique (loosely).  

The idea is to structure your CSS to describe what is being built and where, rather than create particular styles for everything.  The benefits aren't always clear until you look back at your styles months or years later.  It gets messy and less maintable with time.

You may create a simple button:


    <a href="#" id="searchButton" class="button">Search</a>


<a href="#" id="searchButton" class="button">Search</a>

The CSS might look like this...


    #searchButton {
        /* search specific style */
        background-color: #bebdbd;
        background-image: -moz-linear-gradient(top, #E38914, #E36C14);
        background-image: linear-gradient(top, #E38914, #e36c14);
        border-color: #bebdbd #bebdbd #696969;
        border-color: rgba(0, 0, 0, 0.1) rgba(0, 0, 0, 0.1) rgba(0, 0, 0, 0.25);
        text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.25);
        color: #ffffff;
        font-size: 0.85em;	
    }
    
    .button {
        /* generic button style */
        border-radius: 3px;
        border-color: 1px solid #888;
        color: #fff;
        font-weight: 800;
        height: 36px;
        margin: 0;
        padding: 8px 20px 8px;
    }


That doesn't look so bad, but what happens when you start adding more and more buttons to the site?  If someone requests a style change you may have to change that style or your approach.  Styles get complicated as more rules are shared.

    #searchButton,
    #contactButton {
        /* search & contact style */	
    }
    #searchButton {
        /* search only style */	
    }
    #contactButton {
        /* contact only style */	
    }
    
    .btn,
    .sidebar-btn,
    .contact-btn {
        /* generic button style */
    }
    /* Leaving out the visited/hover/active states here */

Trust me, eventually this get's much worse. But there is a better way!  An example of a button from Bootstrap.


    <a href="#" class="btn btn-primary">Search</a>


<a href="#" class="btn btn-primary">Search</a>

To change the appearance you keep adding more classes to give it the look you want (for brevity I'm not including the Bootstrap styles).  If it's a unique look, create a new modular style according to the naming convention and add that class to the element.  Your future self will thank you.


    <!-- simple blue button -->
    <a href="#" class="btn btn-primary">Search</a>
    
    <!-- simple blue LARGE button -->
    <a href="#" class="btn btn-primary btn-large">Search</a>
    
    <!-- custom color button -->
    <a href="#" class="btn btn-primary-specific-situation">Search</a>
    
    <!-- a button appended ont a input field -->
    <div class="input-append">
      <input class="span2" id="appendedInputButton" type="text">  
      <a href="#" class="btn btn-primary">Search</a>
    </div>
    <!-- styles can become very unqiue by adding to the architecture -->


Granted, this styling is easy now because of all the hard work put into Bootstrap.   Don't be discouraged, this can easily be done on any project, big or small, with a little mindfulness of how [SMACSS](http://smacss.com/) works.  It may take some occasional refactoring but creating interfaces will be much easier as the project progresses, saving you time in the long-run.

#### Side Note

I've never heard anyone complain about the potential affect file size this may have on your page.  If ever brought up, I would point to the fact that your biggest gains in site performance would be images and scripts.  Images account for the majority of file transfer time and byte size for a typical website.  The next biggest chunk would be javascript files.  If you care about performance; optimize your photos, concatenate and GZIP your Javascript files, serve all those files over a CDN. 