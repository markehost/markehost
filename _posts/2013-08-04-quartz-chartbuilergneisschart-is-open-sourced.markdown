---
layout: post
title: Quartz Chartbuiler/Gneisschart is Open Sourced
date: '2013-08-04 16:00:00'
---

#### Quick & Dirty Charts

[Quartz](http://qz.com/), the innovative news site recently released a great tool for the public called [Chartbuilder](https://github.com/Quartz/Chartbuilder/).  The creator, David Yanofsky, [announces the library](http://www.niemanlab.org/2013/07/how-to-turn-everyone-in-your-newsroom-into-a-graphics-editor/).  

If you blog or need to create Presentations, it's a great charting tool for non-technical users that need simple charts.  It's much simpler to create than MS Office tools but doesn't come close to replacing it. 

While it's too simple to be a **great** tool, it will assist in providing more sensible data visualizations than the nearly useless pie charts or 3D versions of other chart types you see on news sites.

There's a [public version](http://quartz.github.io/Chartbuilder/) available for use or you can use it locally.  I would like to see improvements to it after being open-sourced and would like to modify the tool to my liking since it uses [D3.js](http://d3js.org/).

Setting it up locally is [super easy](https://github.com/yanofsky/Number-of-Times-You-Have-Consulted-This-Chart--By-Day).

Here are two charts I created quickly.

![Voter Turnout](/content/images/2014/Jan/chart.png)

<p class="caption">Voter Turnout for the last four US Presidential Elections.</p>

![Length of my posts in reading time](/content/images/2014/Jan/chart2.png)

<p class="caption">Estimated length of my posts in reading minutes.</p>


#### Issues with Chartbuilder

* You have to refresh the page often if you are changing chart types, data or attributes.
* The image and SVG tend to produce odd export dimensions, either getting cut off or producing too much white-space.
* It's difficult to control with large data sets.  It's great for small manageable data.
* The chart doesn't expand or contract based on data so labels collide. Additionally the site layout doesn't allow the left panel to scroll potentially rendering it un-useable on small screens. 
* The script obviously isn't accounting for certain customizations and the controllable attributes are limited.



Since this tool uses D3.js it's totally possible to fix these bugs and missing features.  I look forward to the challenge of fixing bugs and adding functionality.