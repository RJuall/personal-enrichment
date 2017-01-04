# How to Use Effects and Animations

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 198

***

## How to Use Effects

Any illusion of movement on a web page can be referred to as *animation*

A *callback function* is coded as the last parameter of an *effect* method so that the function is called after the method finishes

The Basic Methods for jQuery Effects:

  1. `show()` - Display the selected elements from the upper left to the lower right
  2. `hide()` - Hide the selected elements from the lower right to the upper left
  3. `toggle()` - Display or hide the selected elements
  4. `slideDown()` - Display the selected elements with a sliding motion
  5. `slideUp()` - Hide the selected elements with a sliding motion
  6. `slideToggle()` - Display or hide the selected elements with a sliding motion
  7. `fadeIn()` - Display the selected elements by fading them in to opaque
  8. `fadeOut()` - Hide the selected elements by fading them out to transparent
  9. `fadeToggle()` - Display or hide the selected elements by fading them in or out
  10. `fadeTo()` - Adjust the opacity property of the selected elements to the opacity set by the second parameter. With this method, the duration parameter must be specified

The basic syntax for all of the methods except the `fadeTo` method - `methodName([duration][, callback])`

The basic syntax for the `fadeTo` method - `fadeTo(duration, opacity[, callback])`

jQuery that fades a selected element out over 5 seconds - `$("#selector").fadeOut(5000);`

jQuery that uses chaining to fade the heading out and slide it back down - `$("#selector").fadeOut(5000).slideDown(1000);`

Chaining with `fadeTo` methods - `$("#selector").fadeTo(5000, .2).fadeTo(1000, 1);`

jQuery with a callback function that gets the same result as the chaining:

```javascript
$("#selector").fadeTo(5000, .2,
    function() {
        $(this).fadeTo(1000, 1);
    }
);
```

```javascript
//jQuery for the 'faqs' application with effects
$(document).ready(function() {
    $("#faqs h2").click(
        function() {
            $(this).toggleClass("minus");
            if ($(this).attr("class") != "minus") {
                $(this).next().fadeOut(1000);
            } else {
                $(this).next().slideDown(1000);
            }
        }
    );  //end click
});     //end ready
//----------------------------------------------
//Same application, using slideToggle instead
$(document).ready(function() {
    $("faqs h2").click(
        function() {
            $(this).toggleClass("minus");
            $(this).next().slideToggle(1000);
        }
    );  //end click
});     //end ready
```

## A Slide Show Application with Effects

```javascript
//jQuery ver. 1
$(document).ready(function() {
    //create an array of the slide images
    var image, imageCounter = 0, imageCache = [];
    $("#slides img").each(function() {
        image = new Image();
        image.src = $(this).attr("src");
        image.title = $(this).attr("alt");
        imageCache[imageCounter] = image;
        imageCounter++;
    });
    //start slide show
    imageCounter = 0;
    var nextImage;
    setInterval(
        function() {
            $("#caption").fadeOut(1000);
            $("#slide").fadeOut(1000,
                function() {
                    imageCounter = (imageCounter + 1) % imageCache.length;
                    nextImage = imageCache[imageCounter];
                    $("#slide").attr("src", nextImage.src).fadeIn(1000);
                    $("caption").text(nextImage.title).fadeIn(1000);
                }
            );
        },
    3000);
})

//-------------------------------------------
//jQuery ver. 2 with show stop/start
$(document).ready(function() {
    var nextSlide = $("#slides img:first-child");
    var nextCaption;
    var nextSlideSource;

    //the function for running the slide show
    var runSlideShow = function() {
        $("#caption").fadeOut(1000);
        $("#slide").fadeOut(1000,
            function() {
                if (nextSlide.next().length == 0) {
                    nextSlide = $("#slides img:first-child");
                } else {
                    nextSlide = nextSlide.next();
                }
                nextSlideSource = nextSlide.attr("src");
                nextCaption = nextSlide.attr("alt");
                $("slide").attr("src", nextSlideSource).fadeIn(1000);
                $("#caption").text(nextCaption).fadeIn(1000);
            }
        )
    }

    //start slide show
    var timer1 = setInterval(runSlideShow, 3000);

    //starting and stopping the slide show
    $("slide").click(function() {
        if (timer1 != null) {
            clearInterval(timer1);
            timer1 = null;
        } else {
            timer1 = setInterval(runSlideShow, 3000);
        }
    });
})
```

## How to Use Animation

The basic syntax for the animate method - `animate({properties}[, duration][, callback])`

An animate method for the `<h1>` heading without a callback function:

```javascript
$("#faqs h1").animate(
    { fontSize: "275%", opacity: 1, left: 0 },      //the properties map
    2000
);                                                  //end animate
```

An animate method for the `<h1>` heading with a callback function:

```javascript
$("#faqs h1").animate(
    { fontSize: "275%", opacity: 1, left: "+=175" },
    2000,
    function() {
        $("#faqs h2").next().fadeIn(1000).fadeOut(1000);
    }
);                                                  //end animate
```

When the animate method is run, the CSS properties for the selected elements are changed to the properties in the *properties map* that is coded as the first parameter of the method. The animation is done in a phased transition based on the duration parameter.

To specify a property name in the properties map use camel casing instead of CSS hyphenation, or enclose the property name is quotation marks

To specify a non-numeric property value, enclose the value in quotation marks

For measurements, pixels are assumed. `+=` or `-=` can be used with numeric values. These operators or different measures must be enclosed in quotation marks

For some properties, like width, height, and opacity, 'show', 'hide', or 'toggle' can be used as property values. These will show, hide, or toggle the element by setting the property appropriately

Color transitions cannot be acheived with `animate`, though jQuery UI can do this

When chaining effects or animations for a selected element they are placed in the element's *queue*, and the effects and/or animations are executed in sequence

All effects/animations for a particular elemement are placed in the same queue, regardless of what method called those effects

A problem may occur if the user starts a second animation for an element before the callback function for the first animaton has finished

The delay, stop, and finish methods:

  1. `delay(duration)` - Delay the start of the next animation in the queue
  2. `stop([clearQueue][, jumpToEnd])` - Stop the current animation for the selected element. The two parameters are Boolean with false default values. If set to true, the first parameter clears the queue so no additional animations are run. The second parameter causes the current animation to be completed immediately
  3. `finish([queue])` - Stop the current animation for the selected element, clear the queue, and complete all animations for the selected elements

Example of the `stop()` method, stops the queued animations before starting new ones:

```javascript
$("#image_list a").hover(
    function(evt) { $(this).stop(true).animate({ top: 15 }, "fast"); },
    function(evt) { $(this).stop(true).animate({ top: 0  }, "fast"); }
);  //end hover
```

An *easing* determines the way an animation is performed

jQuery provides two easings: linear and swing - there are many more available in jQuery UI

The syntax for all of the basic methods except the `fadeTo` method: `methodName([duration][, easing][, callback])`

The syntax for the `fadeTo` method: `fadeTo(duration, opacity[, easing][, callback])`

The syntax for the basic animate method: `animate({properties}[, duration][, easing][, callback])`

A script element for getting the jQuery UI library from the jQuery CDN:

```html
<!-- the element for jquery ui must come after the one for jquery -->
<script srt="//code.jquery.com/ui/1.11.4/jquery-ui.min.js"></script>
```

```javascript
//two easings used by the 'faqs' application
$("#faqs h2").click(function() {
    $(this).toggleClass("minus");
    if ($(this).attr("class") == "minus") {
        $(this).next().slideDown(1000, "easeOutBounce");
    } else {
        $(this).next().slideUp(1000, "easeInBounce");
    }
});     //end click
```

```javascript
//two easings for an animated heading
$("#faqs h1").click function() {
    $(this).animate(
        { fontSize: "650%", opacity: 1, left: "+=275" }, 2000, "easeInExpo" )
    .animate (
        { fontSize: "175%", left: "-=275" }, 1000, "easeOutExpo" );
});     //end click
```

The advanced syntax for the animate method: `animate({properties}, {options})`

Some of the options for the advanced syntax:

  1. `duration` - A string or number that specifies the duration of the animation
  2. `easing` - A string that specifies an easing function
  3. `complete` - A callback function that runs when the animation is complete
  4. `step` - A function to call after each step that the animation is broken down into
  5. `queue` - A boolean value. If true, the animation will be placed in the queue. If false, the animation will start immediately
  6. `specialEasing` - A map of one or more of the properties in the properties map with their corresponding easings

The methods for working with animation queues:

  1. `queue([name])` - Get the queue for the selected element
  2. `queue([name], newQueue)` - Replace the queue for the selected element with a new queue
  3. `queue([name], callback)` - Add a new function (callback) to the end of the queue for the selected element
  4. `dequeue([name])` - Run the next item in the queue for the selected element
  5. `clearQueue([name])` - Remove all items that haven't yet been run from the queue

An animate method that uses advanced syntax:

```javascript
$("#faqs h1").animate(
    { fontSize: "650%", opacity: 1, left: "+=175" },
    { duration: 2000,
      specialEasing: { fontSize: "easeInExpo", left: "easeOutExpo" },
      complete: function() {
          $("#faqs h2").next().fadeIn(1000).fadeOut(1000); }
    }
);      //end animate
```

```javascript
//how to provide easings by property with the basic syntax
$("#faqs h1").animate(
    { fontSize: ["650%", "easeInExpo"],
      opacity: [1, "swing"],
      left: ["+=275", "easeOutExpo"] }, 2000
);      //end animate
```

The name parameter in the methods for working with queues isn't needed for the default queue (fx), it's only needed for custom queues that are programmer created

## A Carousel Application with Animation

```javascript
//the jQuery for the 'carousel' application
//to get the value of the left property of the <ul> element, the css method is used
//the value of the left property for the <ul> element will range from 0 to -600
$(document).ready(function() {
    var slider = $("#image_list");      //slider = <ul> element
    var leftProperty, newleftProperty;

    //the click event handler to the right button
    $("#right_button").click(function() {

        //get value of current left property
        leftProperty = parseInt(slider.css("left"));

        //determine new value of left property
        if(leftProperty - 300 <= -900) {
            newleftProperty = 0; }
        else {
            newleftProperty = leftProperty - 300; }

        //use the animate method to change the left property
        slider.animate( {left: newleftProperty}, 1000);
    });     //end click

    //the click event handler to the left button
    $("#left_button").click(function() {

        //get value of current left property
        leftProperty = parseInt(slider.css("left"));

        //determine new value of left property
        if (leftProperty < 0) {
            newleftProperty = leftProperty + 300; }
        else {
            newleftProperty = 0; }

        //use the animate method to change the left property
        slider.animate( {left: newleftProperty}, 1000);
    });     //end click
});         //end ready
```

***

### END CHAPTER

Robert Juall

07NOV2016