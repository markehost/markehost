---
layout: post
title: Simple Backbone View Animations
---

Single page apps can be very (link:http://ricostacruz.com/backbone-patterns/#animation_buffer  text:jarring if you're not using animations) to show views with new or detailed views.  Animations in a SPA can be trickier to maintain due to the multiple interactions that ocurr.  I'll display a simple solution.

The quickest way to animate your views in Backbone is using the basic effects built into jQuery.  Your data and views are usually instantly rendered and immediately available.  The key is hiding the view before your user will see it.  We can do that by using inline style or by a CSS class.

~~~~.prettyprint
<!-- using inline style -->
<div class="ChromeDetail" style="display: none;"></div>

<!-- using CSS class -->
<div class="ChromeDetail hidden"></div>
~~~~

Using a class is cleaner, though, the jQuery effects will manipulate style inline anyways.  This is one of the rare cases that I allow use of inline style.

For brevity, I'm just going to show you the Backbone methods I'm modifying.  These methods would normally go inside your view.  

I'll will start with the removal of the view first since that's the easiest because there are less interactions to account for in the view.

~~~~.prettyprint
closeView: function() {
	$('.detail').remove();
}
~~~~

Instead of just removing the view, let's put that code inside a jQuery effects callback function.

~~~~.prettyprint
closeView: function() {
	$(this.detailView.$el).slideUp('50', function() {
	  	$('.detail').remove();
	});
}
~~~~

What I'm doing above is targeting a DOM element, telling it to slideUp within 50 milliseconds and once that's done to remove the DOM element that is supposed to be my detailed view that the user no longer wants to see.

Now let's see the method to show the detailed view.

~~~~.prettyprint
showView: function(e) {
	// remove the detailed view if it exists
	var detail = $('.detail');
	if ( detail.length > 0) {		
		$(detail).remove();
	}
	
	// add the model detail template to the view
	// based on the model that was clicked by user
	modelID = $(e.currentTarget).find(".modelID").text();
	this.detailView = new DetailView({
		model: this.generalView.model.get(modelID)
	});
	// normally this would show if we didn't hide the HTML initially
	$(e.currentTarget).after(this.detailView.$el);
	
}
~~~~

Let's redo the view of showing extra detail with animations.  We have to acount for a detail view already being open, and then animate the new detailed model being displayed within the hidden template.

~~~~.prettyprint
showView: function(e) {
	var ChromeDetail = $('.ChromeDetail');
	if ( ChromeDetail.length > 0) {
		detailView = this.currentDetail.$el;
		$(this.detailedViewToShow.$el).slideUp('50', function() {
		  return $('.categoryDetail').remove();
		});
	}
	
	// add the model detail template to the view
	modelID = $(e.currentTarget).find(".modelID").text();
	this.detailView = new DetailView({
		model: this.generalView.model.get(modelID)
	});
	$(e.currentTarget).after(this.detailView.$el);
	
	// this is where jQuery will animate the height and visibility of the template
	$(this.detailView.$el).slideDown('50', function() {
	  	console.log('finished showing the detailed view');
	});
}
~~~~

There is an issue with the code, we haven't accounted for clicks on the already opened details.  You may have many different scenarios to cover with your Backbone views, but the above example shows how you can use callback functions to show, hide and trigger your functionality.

This is an easy way to accomplish view animation.  A caveat about this is that your code may get sloppy very quickly.  I recommend doing what's best 