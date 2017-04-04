---
layout: post
title: Quartz Chartbuiler/Gneisschart is Open Sourced
---

#### Quick & Dirty Charts

(link: http://qz.com/ text: Qaurtz), the innovative news site recently released a great tool for the public called (link: https://github.com/Quartz/Chartbuilder/ text: Chartbuilder).  The creator, David Yanofsky, (link: http://www.niemanlab.org/2013/07/how-to-turn-everyone-in-your-newsroom-into-a-graphics-editor/ text: announces the library).  

If you blog or need to create Presentations, it's a great charting tool for non-technical users that need simple charts.  It's much simpler to create than MS Office tools but doesn't come close to replacing it. 

While it's too simple to be a **great** tool, it will assist in providing more sensible data visualizations than the nearly useless pie charts or 3D versions of other chart types you see on news sites.

There's a (link: http://quartz.github.io/Chartbuilder/ text: public version) available for use or you can use it locally.  I would like to see improvements to it after being open-sourced and would like to modify the tool to my liking since it uses (link: http://d3js.org/ text: D3.js).

Setting it up locally is (link: https://github.com/yanofsky/Number-of-Times-You-Have-Consulted-This-Chart--By-Day text: super easy).

Here are two charts I created quickly.

(image: chart.png class: chart text: Chart 1 )
<p class="caption">Voter Turnout for the last four US Presidential Elections.</p>

(image: chart2.png class: chart text: Chart 2 )
<p class="caption">Estimated length of my posts in reading minutes.</p>


#### Issues with Chartbuilder

* You have to refresh the page often if you are changing chart types, data or attributes.
* The image and SVG tend to produce odd export dimensions, either getting cut off or producing too much white-space.
* It's difficult to control with large data sets.  It's great for small manageable data.
* The chart doesn't expand or contract based on data so labels collide. Additionally the site layout doesn't allow the left panel to scroll potentially rendering it un-useable on small screens. 
* The script obviously isn't accounting for certain customizations and the controllable attributes are limited.



Since this tool uses D3.js it's totally possible to fix these bugs and missing features.  I look forward to the challenge of fixing bugs and adding functionality.