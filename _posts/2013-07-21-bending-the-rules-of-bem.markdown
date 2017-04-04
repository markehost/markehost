---
layout: post
title: Bending the Rules of BEM
date: '2013-07-21 16:00:00'
---

[OOCSS](https://github.com/stubbornella/oocss) is a growing topic in front-end development.  It spawned a book in [SMACSS](http://smacss.com/), [BEM](http://bem.info/method/definitions/) is a full systems of building structure along with style and more loosely defined approaches such as [MVCSS](http://mvcss.github.io/).  

There are two subtle points that are made throughout these methods that alleviate pain in a project, yet aren't worth strict adherence.

* Avoid particular HTML structure in your object-oriented styles.
* Avoid nesting pre-processed rules beyond 3 levels.

These methods all share the same philosophy of structuring your templates and styles to scale for large apps.  They outline directory structure, class naming convention and define tactics for the organized growth of code.

In practice they have proven immensely helpful, yet strict adherence can cause unintended side-effects to your applications style.

### Avoid Using a Particular HTML Structure

Besides avoiding the side-effect of creating a "classitis" in your markup, associating certain HTML structure with your styles can be a good thing. 

Classic examples in [Twitter Bootstrap](http://twitter.github.io/bootstrap/) syntax.  An extreme case with the [collapse](http://twitter.github.io/bootstrap/javascript.html#collapse) required syntax. 

	<div class="accordion" id="accordion2">
  	<div class="accordion-group">
    	<div class="accordion-heading">
	      <a class="accordion-toggle" data-toggle="collapse" data-parent="#accordion2" href="#collapseOne">
	<!-- closing tags -->  	
	<style>
		.collapse {...}
		.accordion-group {...}
		.accordion-heading {...}
		.accordion-heading .accordion-toggle {...}
		.accordion-inner {...}
	</style>

The above style is more BEM-like, making it free from structure but uses many classes.  If you look at the basic tabs, link list, or the navbar syntax you see structure with less classes.

	<ul class="nav nav-tabs">
	  <li class="active">
    	<a href="#">Home</a>
	  </li>
	  <li><a href="#">...</a></li>
	  <li><a href="#">...</a></li>
	</ul>
	<style>
		.nav-tabs 	 		{...}
		.nav-tabs > li 		{...}
		.nav-tabs > li > a 	{...}
	</style>

These are contrived examples that only account for a limited set of modules, where as in real applications, styles get messy very quickly where there may be several different versions of a module throughout the app.  Additional requests to customize aspects to these common elements style roll in which force you to customize parent &amp; child.   

Using the BEM class naming convention we can achieve the customized result with one class per HTML element, <code>.block-name__element-name--modifier-name</code> for all the parents &amp; children. 

At some point the class creation needs to stop and a strict structure is well suited.  We may need <code>.is-active</code> type classes within the parents, but often markup enforcement can make the style cleaner and specific to those instances of customization.

	<div class="widget__list-item">
		<header>
			<!-- this could be an image and header text -->
		</header>
		<footer>
			<!-- a link list  -->		
		</footer>
	</div>

	<div class="widget__tile-item">
		<header>
			<!-- the same image and header text -->
		</header>
		<footer>
			<!-- a link list -->		
		</footer>
	</div>
	<style>
		/* Less Styles */
		[class*="widget"] {
			/* general widget styles */
			header {}
			footer {}

			&[class*="list-item"] {
				/* list specific style */
			}
			&[class*="tile-item"] {
				/* tile specific style */
			}
		}
	</style>

The point is, you can use specific HTML structure within BEM or object-oriented CSS and still retain the modularity of the class conventions.  By changing the parent class slightly you can tweak the look while keeping the same basic structure.

There are a number of reasons you want to do this, especially on large teams for an expanding CSS code base.

* De-clutter the markup from an extraordinary amount of classes
* Use slightly more semantic structure than generic DIV (with descriptive class name).
* Enforce other developers to use a certain structure (and stop being lazy).

Twitter Bootstrap only contains a few instances, but in practical development you see more cases for writing styles to specific markup structure.



### Avoid Nesting Rules Beyond 3 Levels

This one is more subtle, though, there are good reasons for it's existence.  

* Deep nesting of rules makes for **very** specific markup structure.
* Pre-compiled styles get very hard to read the more levels of nesting you use.
* You can often accomplish the same styles with 3 levels or less.

With the power of CSS precompilers comes an amount of creativity in how you structure your styles.  My primary use case for diverging from this rule is when apps become complex and require a greater level of complexity.  

Using multiple attribute selectors to narrow down a style.  This helps me remove the use of multiple classes and keep the class name to one longer class.

	<div class="block__element--modifier">
		<ul>
			<li><a href="#"></a></li>
			<li><a href="#"></a></li>
		</ul>
	</div>

	<style>
		[class*="block"] {
			[class*="element"] {
				[class*="modifier"] {
					ul {
						li {
							a {}
						}
					}	
				}
			}	
		}
	</style>

That looks ridiculously nested at 6 levels, which could have been accomplished by pulling the nested styles into their own separate line.  Sometimes, there's no need for a certain <code>element</code> or <code>modifier</code> to be on it's own.  It belongs within a parent <code>block</code> style.

The most common case for this is when creating a series of UI widgets that belong under a wrapper class (<code>block</code> level parent in BEM).


### Conclusion

BEM, SMACSS and MVCSS are great.  They're a huge time saver for you, your future self and other front-end devs.  Most rules should be followed strictly to provide consistency, others are more of a guidance to throttle back the differences between UI developers on a project.