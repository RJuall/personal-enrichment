# How to Use the DOM Manipulation and Traversal Methods

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 277

***

## The DOM Manipulation Methods

*DOM manipulation* methods let you get and set attribute values. They also let you replace, insert, copy, wrap, and remove DOM elements.

The methods for working with attributes:

  1. `attr(name)` - Gets the value of the named attribute from the first selected element.
  2. `attr(name, value)` - Sets the value of the named attribute for each selected element.
  3. `attr(map)` - Sets the value of multiple attributes specified by the name/value pairs in the attribute map.
  4. `attr(name, function)` - Sets the value of the named attribute to the value returned be the function.
  5. `removeAttr(name)` - Removes the named attribute from each selected element.

The methods for working with class attributes:

  1. `hasClass(name)` - Returns true if the named class is present in any selected elements.
  2. `addClass(name)` - Adds the named class to each selected element.
  3. `addClass(function)` - Adds the class specified by the value returned by the function.
  4. `removeClass(name)` - Removes the named class from each selected element.
  5. `removeClass(function)` - Removes the class specified by the value returned by the function.
  6. `toggleClass(name)` - If the named class is present, remove it from each selected element. Otherwise, add it.
  7. `toggleClass(function)` - If the class specified by the value returned by the function is present, remove it. Otherwise, add it.

Set the value of the `src` attribute of an image to the value of a variable - `$("#image").attr("src", "book1.jpg");`

Use a map to set the values of two attributes - `$("#image").attr( {"src": "book1.jpg", "alt": "Book 1"} );`

```javascript
//Use a function to set the value of the `href` attribute of each `<a>` element
    $("aside a").attr("href", function(index) {
        var href = "#heading" + (index + 1);
        return href;
    });
```

Test whether an element has a 'closed' value in its class attribute - `if ($("#faqs").hasClass("closed")) {...}`

The methods for DOM replacement:

  1. `val()` - Gets the value of the first selected form element.
  2. `val(value)` - Sets the value of the selected form elements.
  3. `val(function)` - Sets the value of the selected form elements to the value returned by the function.
  4. `text()` - Gets the combined text contents of all selected elements including their descendants.
  5. `text(textString)` - Sets the contents of each selected element to the text returned by the function.
  6. `text(function)` - Sets the contents of each selected element to the text returned by the function.
  7. `html()` - Gets the HTML contents of the first selected element.
  8. `html(htmlString)` - Sets the HTML contents of each selected element to the specified HTML string.
  9. `html(function)` - Sets the HTML contents of each selected element to the HTML string returned by the function.
  10. `replaceWith(content)` - Replaces each selected element with the specified content. This could be an HTML string, a DOM element, or a jQuery object.
  11. `replaceAll(target)` - Replaces each target element with the selected elements. This is the reverse of how the replaceWith method is coded.

Display all of the HTML in the `aside` element - `alert($("aside").html());`

Put an `h2` element into an `aside` element - `$("aside").html("<h2>Table of contents</h2>");`

Replace all elements that have a class named 'old' with an `h2` element - `$(".old").replaceWith("<h2></h2>");`

Replace all elements that have a class named 'old' with an `h2` element - `$("<h2></h2>").replaceAll(".old");`

The methods for DOM insertion and cloning:

  1. `prepend(content)` - Inserts the specified content at the start of each selected element.
  2. `prepend(function)` - Inserts the content returned by the function at the start of each selected element.
  3. `prependTo(target)` - Inserts all of the selected elements at the start of each target element.
  4. `append(content)` - Inserts the specified content at the end of each selected element.
  5. `append(function)` - Inserts the content returned by the function at the end of each selected element.
  6. `appendTo(target)` - Inserts all of the selected elements at the end of each target element.
  7. `before(content)` - Inserts the specified content before each selected element.
  8. `before(function)` - Inserts the content returned by the function before each selected element.
  9. `insertBefore(target)` - Inserts all of the selected elements before each target element.
  10. `after(content)` - Inserts the specified content after each selected element.
  11. `after(function)` - Inserts the content returned by the function after each selected element.
  12. `insertAfter(target)` - Inserts all of the selected elements after each target element.
  13. `clone([withEvents])` - Creates a copy of the selected elements. The parameter is a boolean that indicates if the event handlers are also copied.

Insert an `h2` element at the end of an aside element - `$("aside").append("<h2>Table of contents</h2>");`

Insert an `<a>` element after the last `<p>` element in an article - `$("article p:last").after("<a href='#top'>Back to top</a>");`

Insert the `<a>` elemetns in an article after the `h2` elements in an `aside` - `("article a").insertAfter($("aside h2"));`

Clone the `<a>` elements and insert them after the `h2` element in an aside element - `("article a").clone().insertAfter($("aside h2"));`

The prepend and append methods insert the content at the start or end of hte selected elements, but within the elements.

The before and after methods insert the content before or after the selected elements, not within the selected elements.

The methods for DOM wrapping and removal:

  1. `wrap(element)` - Wraps the specified element around each selected element.
  2. `wrap(function)` - Wraps the element returned by the function around each selected element.
  3. `wrapAll(element)` - Wraps the specified element around all of the selected elements.
  4. `wrapInner(element)` - Wraps the specified element around the content of each selected element.
  5. `wrapInner(function)` - Wraps the element returned by the function around the content of each selected element.
  6. `empty()` - Removes all of the child nodes of each selected element.
  7. `remove([selector])` - Removes the selected elements from the DOM. If a selector is specified, it filters the selected elements.
  8. `unwrap()` - Removes the parent of each selected element.

Wrap all `<a>` elements in `h2` elements - `$("a").wrap("<h2></h2>");`

Wrap the `h1` text in an `<a>` element - `$("article h1").wrapInner("<a id='top'></a>");`

Remove the first `<a>` element in an article - `$("article a:first").remove();`

## The TOC Application

The jQuery plan:

  1. Add the `h2` element for the 'Table of Contents' heading to the aside.
  2. Wrap the text of the `h2` elements in the article with the `<a>` elements.
  3. Add the correct id attributes to the `<a>` elements in the article.
  4. Clone the `<a>` elements in the article and insert them after the `h2` element in the `aside`.
  5. Remove the id attributes from the `<a>` elements in the `aside`.
  6. Add the correct href attributes to the `<a>` elementss in the `aside`.
  7. Wrap an `<a>` element with 'top' as its id around the text in the `h1` element.
  8. Insert `<a>` elements that go to the `h1` element at the end of each topic.

```javascript
$(document).ready(function() {
    // add an h2 heading to the aside
    $("aside").append("<h2>Table of contents</h2>");

    // wrap the h2 text in the article with <a> tags
    $("article h2").wrapInner("<a></a>");

    // add ids to the new <a> tags
    $("article a").each(function(index) {
        var id = "heading" + (index + 1);
        $(this).attr("id", id);
    });

    // clone the <a> tags in the article and insert them into the aside
    $("article a").clone().insertAfter($("aside h2"));

    // remove the id attributes from the <a> tags in the aside
    $("aside a").removeAttr("id");

    // add the href attributes to the <a> tags in the aside
    $("aside a").attr("href", function(index) {
        var href = "#heading" + (index + 1);
        return href; 
    });

    // wrap an <a> tag around the h1 text
    $("h1").wrapInner("<a id='top'></a>");

    // insert "back to top" <a> tags after each topic
    $("article h2").before("<a href='#top'>Back to Top</a>");
    $("article a:first").remove();
    $("article p:last").after("<a href='#top'>Back to Top</a>");
})
```

## The Methods for Working with Styles and Positioning

The methods for working with styles:

  1. `css(name)` - Gets the value of the named property from the first selected element.
  2. `css(name, value)` - Sets the value of the named property for each selected element.
  3. `css(map)` - Sets the values of multiple properties specified by the name/value pairs in the properties map.
  4. `css(name, function)` - Sets the value of the named property to the value returned by the function.
  5. `height()` - Gets the height of the first selected element. This height doesn't include padding, margins or borders.
  6. `height(value)` - Sets the height of the first selected element.
  7. `innerHeight()` - Gets the height of the first selectd element including padding, but not margins or borders.
  8. `outerHeight([includeMargin])` - Gets the height of the first selected element including padding and borders. If the parameter is set to true, it also includes margins.
  9. `width()` - Gets the width of the first selected element. This width doesn't include padding, margins, or borders.
  10. `width(value)` - Sets the width of each selected element.
  11. `innerWidth()` - Gets the width of the first selected element including padding, but not margins or borders.
  12. `outerWidth([includeMargin])` - Gets the width of the first selected element including padding and borders. If the parameter is set to true, it also includes margins.

Set the CSS color property for all `h2` elements to blue - `$("h2").css("color", "blue");`

Use a map to set two CSS properties for all `h2` elements - `$("h2").css( { "color": "blue", "font-size": "150%" } );`

Get the height of an `article` element - `var height = $("article").height();`

When a height/width value is returned it is returned as a number and pixels are assumed.

The methods for positioning elements:

  1. `offset()` - Gets the coordinates of the first selected element and returns them in an object with top and left properties. These coordinates are relative to the document.
  2. `offset(coordinates)` - Sets the coordinates of each selected element relative to the document. The parameter is an object with top and left properties.
  3. `position()` - Gets the coordinates of the first selected element and returns them in an object with top and left properties. These coordinates are relative to the parent element.
  4. `scrollTop()` - Gets the position of the vertical scroll bar for the first selected element.
  5. `scrollTop(value)` - Sets the position of the vertical scroll bar for each selected element.
  6. `scrollLeft()` - Gets the position of the horizontal scroll bar for the first selected element.
  7. `scrollLeft(value)` - Sets the position of the horizontal scroll bar for each selected element.

Get the top offset for an `article` element - `var offsetTop = $("article").offset().top;`

```javascript
// Set the offset coordinates for an aside element
var asideCoordinates = new Object();
asideCoordinates.top = 200;
asideCoordinates.left = 100;
$("aside").offset(asideCoordinates);
```

Move the scroll bar for the window to the top - `$(window).scrollTop(0);`

The scroll methods apply to window objects, elements with the overflow CSS property set to scroll, and elements with the overflow property set to auto if the height to the elements are smaller than their contents.

```javascript
// The jQuery for the enhanced ToC application
//  demonstrating some of the new methods
// The position property for the aside must be either relative or absolute

// change the CSS for the selected topic and move the TOC
$("aside a").click(function() {
    // get the id selector of the selected h2 element from the <a> tag
    id = $(this).attr("href");

    // change the styles for the selected heading
    $(id).css({ "color": "blue", "font-size": "150%" });

    // move the aside so it is next to the selected heading
    var h2Offset = $(id).offset().top;          // get top offset of the h2
    var asideHeight = $("aside").height();      // get height of aside
    var articleHeight = $("article").height();  // get height of article
    if ((h2Offset + asideHeight) <= articleHeight) {
        asideOffset = h2Offset;
    } else {
        asideOffset = articleHeight - asideHeight;
    }
    $("aside").css("top", asideOffset);
});
```

## Two Event Methods Used with DOM Manipulation

Two event methods used with DOM manipulation:

  1. `on(events[, selector], handler)` - Attach an event handler to one or more events of the selected elements.
  2. `off(events[, selector][, handler])` - Remove an event handler from one or more events.

```javascript
//A click event method that handles the click event of an `h2` element
$("#accordion h2").click(function() {
    // the code for the event handler    
});
```

```javascript
//An on event method that handles the click  event of an h2 element
$("#accordion").on("click", "h2", function() {
    // the code for the event handler
});
```

An off event method that removes the first click event handler above - `$("#accordion").off("click");`

An off event method that removes the second click event handler above - `$("#accordion").off("click", "h2");`

When a 'shortcut' event method like `click` or `mouseover` is used to attach an event handler, the `on` method is used internally - `on(event, handler)`, an event handler that's attached in this way is referred to as being *directly bound*

Works only for events that exist in the DOM when the event handler is attached.

The `on` event also lets one execute an event handler for elements even if they don't exist when the event handler is attached.

To do this, attach the handler to one or more events of a parent element that does exist. Then, include the selector for the descendant elements for the element where the event is to be triggered. This is referred to as a *delegated* event handler.

```javascript
//The jQuery for the 'Employee List' application
$(document).ready(function() {

    $("#accordion").on("click", "h2", function() {
        $(this).toggleClass("minus");
        if ($(this).attr("class") != "minus") {
            $(this).next().hide();
        }
        else {
            $(this).next().show();
        }
    }) // end click

    $("#add").click(function() {
        var html = "";
        html += "<h2><a href='#'>" + $("#name").val() + "</a></h2>";
        html += "<div><h3>" + $("#position").val() + "</h3>";
        html += "<p>" + $("#description").val() + "</p></div>";
        $("#accordion").append(html);
        $("#name").val("");
        $("#position").val("");
        $("#description").val("");
    }); // end click
});     // end ready
```

## The DOM Traversal Methods

The tree traversal methods:

  1. `siblings([selector])` - Gets teh siblings of each selected element, optionally filtered by a selector.
  2. `next([selector])` - Gets the first sibling that follows each selected element, optionally filtered by a selector.
  3. `nextAll([selector])` - Gets all siblings that follow each selected element, optionally filtered by a selector.
  4. `nextUntil(selector)` - Gets all siblings that follow each selected element, up to but not including the element specified by the selector.
  5. `prev([selector])` - Gets the first sibling that precedes each selected element, optionally filtered by a selector.
  6. `prevAll([selector])` - Gets all siblings that precede each selected element, optionally filtered by a selector.
  7. `prevUntil(selector)` - Gets all siblings that precede each selected element, up to but not including the element specified by the selector.
  8. `children([selector])` - Gets the children of each selected element, optionally filtered by a selector.
  9. `parents([selector])` - Gets the ancestors of each selected element, optionally filtered by a selector.
  10. `parentsUntil(selector)` - Gets the ancestors of each selected element, up to but not including the element specified by the selector.
  11. `parent([selector])` - Gets the parent of each selected element, optionally filtered by a selector.
  12. `offsetParent()` - Gets the closest ancestor of an element that is positioned.
  13. `closest(selector[, context])` - Gets the first element that matches the specified selector, beginning at the current element and going up the DOM tree. If the context parameter is specified, it specifies a DOM element within which the selected element must be found.
  14. `find(selector)` - Gets the descendants of each selected element after it has been filtered by the specified selector.

Get the previous paragraph sibling of an element - `var previousParagraph = $("#last_heading").prev("p");`

Get the parent of an element - `var parent = $("#faqs").parent();`

Get all span elements within `<p>` elements within an article element - `$("article p").find("span").css("color", "red");`

The tree traversal methods help select the siblings, children, parents, and ancestors of selected elements in the DOM.

In many cases the filtering methods duplicate the results the results that one can get with normal selectors/with the `find` method.

One benefit of filtering methods is that they facilitate chaining.

The filtering methods:

  1. `filter(selector)` - Reduces the set of selected elements to those that match the selector.
  2. `filter(function)` - Reduces the set of selected elements to those that pass the function's test.
  3. `not(selector)` - Removes the elements specified by the selector from the set of selected elements.
  4. `not(elements)` - Removes the specified elements from the set of selected elements.
  5. `not(function)` - Removes the elements that pass the function's test from the set of selected elements.
  6. `has(selector)` - Reduces the set of selected elements to those that have a descendant that matches the selector.
  7. `eq(index)` - Reduces the set of selected elements to the one at the specified index.
  8. `first()` - Reduces the set of selected elements to the first one in the set.
  9. `last()` - Reduces the set of selected elements to the last one in the set.
  10. `slice(start[, end])` - Reduces the set of selected elements to those within the range of indexes that are apecified by the parameters.
  11. `end()` - Returns the set of selected elements to its previous state.

Change a property for the `h2` elements that are in the 'best' class - `$("h2").filter(".best").css("color", "red");`

Change a property for all `<p>` elements except the ones in the 'first' class - `$("p").not(".first").css("text-indent", "1.5em");`

Hide all images in the 'slides' element except for the one with index 0 - `$("#slides img").slice(1).hide();`

```javascript
// Work with the images in a set
$("#slides img")
    .first().fadeOut(1000)      // fade out first img element in set
    .next().fadeIn(1000)        // fade in the next element in set
    .end()                      // return to first element in set
    .appendTo("#slides");       // append first element to end of set
```

```javascript
// 2 ways of writing jQuery for a slide show application
//#slides img must be set to `position: absolute`

// 1st way
$(document).ready(function() {
    $("#slides img").slice(1).hide();
    setInterval(function() {
        $("#slides img").first.fadeOut(1000)    // fade out 1st image
        .next().fadeIn(1000)                    // fade in next image
        .end()                                  // return object to 1st image
        .appendTo("#slides");                   // move 1st image to last
    }, 3000);
});

// 2nd way
$(document).ready(function() {
    $("#slides img").slice(1).hide();
    var slideIndex = 0, topIndex = $("#slides img").length - 1;
    setInterval(function() {
        $("#slides img").eq(slideIndex).fadeOut(1000);
        if (slideIndex < topIndex) {
            $("#slides img").eq(slideIndex).next().fadeIn(1000);
            slideIndex++
        } else {
            $("#slides img").eq(0).fadeIn(1000);
            slideIndex = 0;
        }
    }, 3000);
});
```

***

### END CHAPTER

Robert Juall

21NOV2016