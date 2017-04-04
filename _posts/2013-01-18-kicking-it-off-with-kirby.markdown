---
layout: post
title: Kicking it Off With Kirby
date: '2013-01-18 17:00:00'
---

My relationship with [Stacy](http://www.staceyapp.com/) didn't last long once I tried to add preformatted code beyond simple HTML.  I didn't have the time to fix the parsing errors. I had to find an aletrnative and it had to meet my simple taste for a CMS.  I wanted the following:

- Flat file, no-database structure
- Use of Markdown for text markup
- Solid support of preformatted text within Markdown
- An active community around the project

#### Problems with Stacy

I had to cut it off between me and Stacy.  The deal breaker was the lack of support for preformatted text.  The quick solution was to create Github Gists for every piece of code, but that just became ridiculous.  I seemed to over-look a lot of Stacy's flaws because it was free.  

- Lack of easy extensibility that I missed from WordPress (short-codes and custom attributes)
- Lack of recent updates to the framework (last update was 5 months ago)
- Low level of community support to improve the framework, templates and extensions


#### And Then There Were Two

The choices came down to two premium no-database CMS's, [Statamic](http://statamic.com/) and [Kirby](http://getkirby.com/). Statamatic had some [very popular users](http://statamic.com/gallery) behind it, with mostly the same structure as Stacy and Kirby.  Though, it wasn't open sourced.

Kirby hosts all of the code on Github, with some contributions from individual developers. I was going with Kirby mostly because of the github community.  

The payment structure was similar to [Sublime Text 2](http://www.sublimetext.com/2), you can technically use it indefinitely with all the features for free, but the license requires a purchase to use it.  The $39 would be an investment and more of a thank you to the developer.

### Making the Switch to Kirby

Installing Kirby was easy. Mac OS X comes with PHP and Apache pre-installed so it was only a few steps to get local development going. 

- turn on the Web Sharing in <code>System Preferences -> Sharing</code>
- placing the files in the right directory, <code>Library\WebServer\Documents</code>
- make sure you [show hidden files](http://www.jasonrpoteet.com/2013/01/07/showhide-files-in-osx/) so you can edit the <code>.htaccess</code> file.
 
Open a browser with <code>http://localhost/</code> and everything was mostly working.  You need to change your URL and Subfolder values within the <code>site\config\config.php</code> file, but if you change [templates](http://getkirby.com/downloads), Kirby will give you instructions within the browser on what to change.  If you keep the default template, this [post on installing Kirby](http://getkirby.com/blog/mamp) will help you complete setup.  I'm starting out with [Monochrome](http://monochrome.niklausgerber.com/) for now.

#### Baby Steps

I'm going to walk through the first few steps I took to get up and running.  First, let's upgrade to a more robust Markdown parser.

- Downloaded [PHP Markdown Extra](http://michelf.ca/projects/php-markdown/)
- Copy the file contents from PHP Markdown Extra and past it into the <code>kirby\parsers\markdown.extra.php</code> within Kirby
- Open up the Kirby configuration file located at <code>site\config\config.php</code> in a text editor. Find the following line located around line 157:

	c::set('markdown.extra', false);

Change it to this:

	c::set('markdown.extra', true);

Next up, a few changes to the <code>header.php</code> file.  

	<!doctype html>
	<html itemscope itemtype="http://schema.org/">
	<head>

Change the first few lines to the following:

	<!DOCTYPE html>
	<!--[if lt IE 7]>      <html class="no-js lt-ie9 lt-ie8 lt-ie7" lang="en"> <![endif]-->
	<!--[if IE 7]>         <html class="no-js lt-ie9 lt-ie8" lang="en"> <![endif]-->
	<!--[if IE 8]>         <html class="no-js lt-ie9" lang="en"> <![endif]-->
	<!--[if gt IE 8]><!--> <html class="no-js" lang="en" itemscope itemtype="http://schema.org/"> <!--<![endif]-->
	<head>


Lastly, I added [Modernizr](http://modernizr.com/) for good measure.  Add a PHP script tag right before the closing <code>head</code> tag.  

	<!-- Modernizr -->
	<?php echo js('assets/js/modernizr-2.6.2.min.js') ?>
	</head>

Configure your Modernizr build however you want, I usually just stick to the CSS3 detection, a few of the HTML5 and leave it at that.  The rest is overkill.

That was it for getting this site going.  Kirby is for the most part pretty modern and has plenty of good starter templates.  This site is now running Kirby.