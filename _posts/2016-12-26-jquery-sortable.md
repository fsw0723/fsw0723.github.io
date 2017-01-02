---
layout: post
title: "jQuery sortable with responsive UI and touch device support"
date: 2016-12-26 21:58:00 +0800
categories: front-end
---

I need to build a image previewer as part of an web app which allows drag and drop for sorting. 
The previewer requires to support IE9+ and touch devices.
As the application is using VueJS, the previewer should be able to plug into it.

I have tried a few available solutions:

* **Sortable js**

It works perfect on desktop and supports VueJS.
However on touch devices, the background moves while dragging, which brings a terrible user experience.

Update: This is a bug for ios10, [reference](https://github.com/RubaXa/Sortable/issues/973).

To fix this issue, add event listener for touchmove event.

Demo: [http://rubaxa.github.io/Sortable/](http://rubaxa.github.io/Sortable/)

* **touch-dnd**

It is nice on touch devices but not working on IE9.

Demo: [http://ma.rkusa.st/touch-dnd/](http://ma.rkusa.st/touch-dnd/)

* **jQuery UI sortable**

jQuery UI itself does not have touch support. 
With the help of **jQuery UI Touch Punch**, touch events will be listened. 
This combination supports all my requirements so I decided to choose it.

jQuery UI Touch Punch Demo: [http://touchpunch.furf.com/content.php?/sortable/default-functionality](http://touchpunch.furf.com/content.php?/sortable/default-functionality)

Unlike the example provided by touch punch, my previewer needs to show images in 2 columns, where Bootstrap grid system is used.

{% highlight html %}

<div id="sortable" class="container">
  <div class="row content">
    <div class="col-sm-6">
      <img src="building1.jpg" class='img-responsive photo' alt="">
    </div>
    <div class="col-sm-6">
      <img src="building2.jpg" class='img-responsive photo' alt="">
    </div>
    <div class="col-sm-6">
      <img src="building3.jpg" class='img-responsive photo' alt="">
    </div>
    <div class="col-sm-6">
      <img src="building4.jpg" class='img-responsive photo' alt="">
    </div>

  </div>
</div>
        
{% endhighlight %}
As a image previewer, I want to have a placeholder while dragging the image. So I add a placeholder.

{% highlight javascript %}

placeholder: {
    element: function (currentItem) {
      return $("<div class='ui-state-highlight'><div></div></div>")[0];
    },
    update: function(container, p) {
      return;
    }
}
{% endhighlight %}

{% highlight css %}

.ui-state-highlight{
	padding: 0 15px;

}
.ui-state-highlight>div {
	background: #ddd;
	height: 100%;
}
{% endhighlight%}

The page is responsive thus there is no fixed height and width being set. 
The size of placeholder needs to be changed accordingly as well.

{% highlight javascript %}

over: function(event, ui) {
    var placeholderHeight = ui.item.innerHeight();
    ui.placeholder.height(placeholderHeight);
    var cl = ui.item.attr('class');
    $('.ui-state-highlight').addClass(cl);
},
        
{% endhighlight %}

The code looks all correct but sometimes there will be misalignment after dragging a image. 
After some debugging, the issue found is the inaccuracy of placeholder height. 
For example, if the image height is 110.6px, *ui.item.innerHeight()* will return 111px and set this value to placeholder, thus mismatch with other image items.

To fix this, I manually set the height to all image items as well (like a hack). 
The height styling will be removed when finish dragging. 
This height difference won't be noticed as it's less than 0.5px.

{% highlight javascript %}

start: function( event, ui ) {
    $('.row > div').height(ui.item.innerHeight());
},
stop: function(event,ui){
    $('.row > div').height('auto');
}

{% endhighlight %}

With the above configuration, it looks good now! 

Update1: Another option is clone the current element to be the placeholder.

{% highlight javascript %}
ui.placeholder.html(ui.item.html());
{% endhighlight %}

{% highlight css %}
.ui-state-highlight {
    opacity: 0.3;
}
{% endhighlight %}

Update2: There is a problem when integrating with VueJS and trying to update the original image list order using

{% highlight javascript %}
this.photos.splice(endingIndex, 0, this.photos.splice(startingIndex, 1)[0]);
{% endhighlight %}

The DOM element order won't be changed after adding the above list re-ordering into **stop** callback.


<br /><br /><br />


[Demo](http://htmlpreview.github.io/?https://raw.githubusercontent.com/fsw0723/jquery-sortable-responsive/master/index.html)

[Source code](https://github.com/fsw0723/jquery-sortable-responsive)

Inspirations: 

* [Draggable Elements That Push Others Out Of Way](https://css-tricks.com/draggable-elements-push-others-way/)
* [JS Fiddle example](http://jsfiddle.net/kmb23z36/3/)




