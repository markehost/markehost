---
layout: post
title: Using Comparator For Sorting Backbone Collections
date: '2013-02-24 17:00:00'
author: Mark Host
---

The [comparator method](http://backbonejs.org/#Collection-comparator) in Backbone is quite useful and is only limited by your imagination.  The [Backbone documentation](http://backbonejs.org/) doesn't give us any sample code, so here are a few handy examples.

Use comparator as a method within your collection.  Here I am going to order the models within the collection by ID.

	comparator: function(item) {
    	return item.get("id");
	},


Or for ordering models within a collection by date.



	comparator: function(item) {
    	var date = new Date( 	item.get("preformattedDate") );
	    return -date.getTime(); 
	},

I'm using the minus sign to reverse the order since in this case I want the most recent models by date first.

Or if you want to sort your collection using multiple fields.

	comparator: function(item) {
		return [item.get("lastName"), item.get("firstName")]; 
	},

There are endless possibilities for using the comparator method.  You can use conditionals to return different comparators based on a user selection, the current state or navigational state.  