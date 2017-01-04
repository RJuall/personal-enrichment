# jQuery Essentials

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 155

***

## Introduction to jQuery

*jQuery* is a free, open-source Javascript library that provides dozens of methods for common web features that make Javascript programming easier

One key advantage to jQuery is that all of its functions are tested for cross-browser functionality

jQuery uses CSS selectors to select HTML elements

```javascript
//jQuery for the 'faqs' app
$(document).ready(function() {
    $("#faqs h2").click(function() {
        $(this).toggleClass("minus");
        if($(this).attr("class") != "minus") {
           $(this).next().hide();
        }
        else {
           $(this).next().show();
        }
    });     //end click
});         //end ready
```

jQuery also provides the *jQuery UI* library, which includes functions to build advanced features such as themes, effects, widgets, mouse interactions, etc.

jQuery also includes support for *plugins*

Some typical plugin functions include data validation, slide shows, and carousels

## The Basics of jQuery Programming

A *content delivery network (CDN)* is a web server that hosts open-source software

The first part to coding jQuery is selecting the element or elements to apply a jQuery method to, using jQuery *selectors*

`$("selector")`

How to select elements:

  1. All `<p>` elements in the entire document - `$("p")`
  2. All div elements that are adjacent siblings of h2 elements - `$("h2 + div")`
  3. The element with 'faqs' as its id - `$("#faqs")`
  4. All elements with 'minus' as a class - `$(".minus")`
  5. All `<p>` elements that are descendants of the main element - `$("faqs p")`
  6. All `<p>` elements that are siblings of ul elements - `$("ul ~ p")`
  7. Multiple selectors - `$("#faqs li, div p")`

Some common jQuery methods:

  1. `val()` - Get the value of a text box or other form control
  2. `val(value)` - Set the value of a text box or other form control
  3. `text()` - Get the text of an element
  4. `text(value)` - Set the text of an element
  5. `next([type])` - Get the next sibling of an element or the next sibling of a specified type if the parameter is coded
  6. `submit()` - Submit the selected form
  7. `focus()` - Move the focus to the selected form control or link

If a jQuery selector for a method selects more than one element, jQuery applies the method to all of the elements so a loop is not needed

With jQuery, one uses *event methods* to attach event handlers to events

```javascript
$(selector).eventMethodName(function () {
    // event handler statements
});
```

Two common jQuery event methods: `ready(handler)`, `click(handler)`

The jQuery `ready()` event is superior to Javascript's onload event because `ready()` is triggered as soon as the DOM is built and does not wait for image load, for example

`$(document).ready(function () {});` can also be expressed as `$(function () {});` as `(document).ready` will be assumed

## The Email List Application in jQuery

```javascript
$(document).ready(function() {
    $("#join_list").click(function() {
        var emailAddress1 = $("#email_address1").val();
        var emailAddress2 = $("#email_address2").val();
        var isValid = true;

        //validate the 1st email address
        if (emailAddress1 == "") {
            $("#email_address1").next().text("This field is required.");
            isValid = false;
        } else {
            $("#email_address1").next().text("");
        }

        //validate the 2nd email address
        if (email_address2 == "") {
            $("#email_address2").next().text("This field is required");
            isValid = false;
        } else if (emailAddress1 != email_address2) {
            $("#email_address2").next().text("This entry must equal first entry");
            isValid = false;
        } else {
            $("#email_address2").next().text("");
        }

        //validate the first name entry
        if ($("#first_name").val() == "") {
            $("#first_name").next().text("This field is required");
            isValid = false;
        } else {
            $("#first_name").next().text("");
        }

        //submit form if all entries are valid
        if (isValid) {
            $("#email_form").submit();
        }
    }); //end click
    $("#email_form").submit();
}); //end ready
```

## A Working Subset of Selectors, Methods, and Event Methods

A summary of the most useful jQuery selectors:

  1.  `[attribute]`         - All elements with the named attribute
  2.  `[attribute=value]`   - All elements with the named attribute and value
  3.  `:contains(text)`     - All elements that contain the specified text
  4.  `:empty`              - All elements with no children including text nodes
  5.  `:eq(n)`              - The element at index n within the selected set
  6.  `:even`               - All elements with an even index within the selected set
  7.  `:first`              - The first element within the set
  8.  `:first-child`        - All elements that are first children of their parent elements
  9.  `:gt(n)`              - All elements within the selected set that have an index greater than n
  10. `:has(selector)`      - All elements that contain the element specified by the selector
  11. `:header`             - All elements that are headers (h1, h2, etc.)
  12. `:hidden`             - All elements that are hidden
  13. `:last`               - The last element within the selected set
  14. `:last-child`         - All elements that are the last children of their parent elements
  15. `:lt(n)`              - All elements within the selected set that have an index less than n
  16. `:not(selector)`      - All elements that aren't selected by the selector
  17. `:nth-child`          - All elements that are the nth children of their parent elements
  18. `:odd`                - All elements with an odd index within the selected set
  19. `:only-child`         - All elements that are the only children of their parent elements
  20. `:parent`             - All elements that are parents of other elements, including text nodes
  21. `:text`               - All input elements with the type attribute set to 'text'
  22. `:visible`            - All elements that are visible

`li` elements that are the first child of their parent element - `$("li:first-child")`

Even `tr` elements of a table - `$("table > tr:even")`

Third descendant `<p>` element of an element - `$("#faqs p:eq(2)")`

All input elements with 'text' as the type attribute - `$(":text")`

A summary of the most useful jQuery methods:

  1. `next([selector])` - Get the next sibling of each selected element or the first sibling of a specified type if the parameter is coded
  2. `prev([selector])` - Get the previous sibling of each selected element or the previous sibling of a specified type if the parameter is coded
  3. `attr(attributeName)` - Get the value of the specified attribute from the first selected element
  4. `attr(attributeName, value)` - Set the value of the specified attribute for each selected element
  5. `css(propertyName)` - Get the value of the specified property from the first selected element
  6. `css(propertyName, value)` - Set the value of the specified property for each selected element
  7. `addClass(className)` - Add one or more classes to the selected elements and, if necessary, create the class. If you use more than one class as the parameter, separate them with spaces
  8. `removeClass([className])` - Remove one or more classes. If you use more than one class as the parameter, separate them with spaces
  9. `toggleClass(className)` - If the class is present, remove it. Otherwise, add it
  10. `hide([duration])` - Hide the selected elements. The duration parameter can be "slow", "fast", or a number giving the time in milliseconds. "slow" is 600 milliseconds and "fast" is 200 milliseconds
  11. `show([duration])` - Show the selected elements, the duration paramter works the same as above
  12. `each(function)` - Run the function for each element in an array

Get the value of the src attribute of an image - `$("#image").attr("src");`

Set the value of the src attribute of an image to the value of a variable - `$("#image").attr("src", imageSource);`

Set the value of the color property of the h2 elements to blue - `$("h2").css("color", "blue");`

Add a class to the h2 descendants of the 'faqs' element - `$("#faqs h2").addClass("minus");`

Run a function for each `<a>` element within an 'image_list' element:

```javascript
$("#image_list a").each(function() {
    //The statements of the function
});
```

A summary of the most useful jQuery event methods:

  1. `ready(handler)` - The handler runs when the DOM is built
  2. `unload(handler)` - The handler runs when the user closes the browser window
  3. `error(handler)` - The handler runs when a Javascript error occurs
  4. `click(handler)` - The handler runs when the selected element is clicked
  5. `dblclick(handler)` - The handler runs when the selected element is double-clicked
  6. `mouseenter(handler)` - The handler runs when the mouse pointer enters the selected element
  7. `mouseover(handler)` - The handler runs when the mouse pointer moves over the selected element
  8. `mouseout(handler)` - The handler runs when the mouse pointer moves out of the selected element
  9. `hover(handlerIn, handlerOut)` - The first event handler runs when the mouse pointer moves into an element. The second event handler runs when the mouse pointer moves out
  10. `event.preventDefault()` - Stops the default action of an event from happening

A handler for the double-click event of all text boxes that clears the clicked box:

```javascript
$(":text").dblclick(function () {
    $(this).val("");
});
```

A handler for the hover event of each img element within a list:

```javascript
$("#image_list img").hover(
    function() {
        alert("The mouse pointer has moved into an img element");
    },
    function() {
        alert("The mouse pointer has moved out of an img element");
    }
);      //end hover
```

A preventDefault method that stops the default action of an event:

```javascript
$("#faqs a").click(function(evt)        //the event object is named evt
{
    evt.preventDefault();               //the method is run on the event object
});                                     //end click
```

Other events methods to be aware of:

  1. `on(events, handler)` - Attach an event handler to one or more events
  2. `off(events, [handler])` - Remove an event handler from one or more events
  3. `one(event, handler)` - Attach an event handler and remove it after it runs one time
  4. `trigger(event)` - Trigger the event for the selected element
  5. `bind(event, handler)` - Attach an event handler to an event
  6. `unbind(event, [handler])` - Remove an event handler from an event

How to attach an event handler to an event:

with the on method: `$("#clear").on("click", function() {...});`

with the shortcut method: `$("#clear").click(function() {...});`

How to attach an event handler to two different events:

of the same element - `$("image_list img").on("click mouseover", function() {...});`

of two different elements:

```javascript
var clearClick = function() {...}
$("#clear").click(clearClick);
$(":text").dblclick(clearClick);
```

How to remove an event handler from an event - `$("#clear").off("click");`

How to attach and remove an event handler so it runs only once - `$("#clear").one("click", function() {...});`

How to trigger an event:

with the trigger method - `$("#clear").trigger("click");`

with the shortcut method - `$("#clear").click();`

How to use the shortcut method to trigger an event from an event handler:

```javascript
$(":text").dblclick(function() {
    $("#clear").click();        //triggers the click event of the clear button
});
```

## Three Illustrative Applications

```javascript
//jQuery for the 'faqs' application
$(document).ready(function() {
    $("#faqs h2").click(function() {
        $(this).toggleClass("minus");
        if ($(this).attr("class") != "minus") {
            $(this).next().hide();
        } else {
            $(this).next().show();
        }
    }); //end click
});     //end ready
```

```javascript
//jQuery for the 'image swap' application
$(document).ready(function() {
    //preload images
    $("#image_list a").each(function() {
        var swappedImage = new Image();
        swappedImage.src = $(this).attr("href");
    }); //end preload

    //set up event handlers for links
    $("#image_list a").click(function(evt) {
        //swap image
        var imageURL = $(this).attr("href");
        $("#image").attr("src", imageURL);

        //swap caption
        var caption = $(this).attr("title");
        $("#caption").text(caption);

        //cancel the default action of the link
        evt.preventDefault();   //jQuery cross-browser method
    }); //end click
    $("li:first-child a").focus();
});     //end ready
```

```html
<!--The HTML for the 'image rollover' application-->
<main>
    <h1>Ram Tap Combined Test</h1>
    <ul id="image_rollovers">
        <li><img src="images/h1.jpg" alt="" id="images/h4.jpg"></li>
        <li><img src="images/h2.jpg" alt="" id="images/h5.jpg"></li>
        <li><img src="images/h3.jps" alt="" id="images/h6.jpg"></li>
    </ul>
</main>
```

```javascript
//The jQuery for the 'image rollover' application
$(document).ready(function() {
    $("#image_rollovers img").each(function() {
        var oldURL = $(this).attr("src");   //gets the 'src' attribute
        var newURL = $(this).attr("id");    //gets the 'id' attribute

        //preload rollover image
        var rolloverImage = new Image();
        rolloverImage.src = newURL;

        //set up event handlers
        $(this).hover(
            function() {
                $(this).attr("src", newURL);    //sets the src attribute
            },
            function() {
                $(this).attr("src", oldURL);    //sets the src attribute
            }
        );  //end hover
    });     //end each
});         //end ready

***

### END CHAPTER

Robert Juall

07NOV2016