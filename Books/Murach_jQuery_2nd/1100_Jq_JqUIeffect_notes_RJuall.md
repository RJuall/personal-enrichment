# How to Use jQuery UI Interactions and Effects

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 349

***

## How to Use Interactions

The Five jQuery UI Interactions:

  1. Draggable
  2. Droppable
  3. Resizable
  4. Selectable
  5. Sortable

The draggable and droppable interactions can be used with any HTML element.

A droppable element defines the area where a draggable element can be dropped.

To control what happens when a draggable object is dropped, you can code a callback function for the drop event of the droppable object.

```html
<!-- The HTML for the draggable and droppable elements -->
<div id="vprospect"><img src="images/vprospect.png"></div>
<div id="vconvert"><img src="images/vconvert.png"></div>
<div id="vretain"><img src="images/vretain.png"></div>

<div id="cart"><ul></ul></div>
```

```javascript
//The jQuery for the interactions
$(document).ready(function() {
    $("#vprospect, #vconvert, #vretain").draggable({ cursor: "move" });
    $("#cart ul").droppable({
        drop: function(event, ui) {
            $("<li></li>").html(ui.draggable.children()).appendTo(this);
        }
    });
});
```

```html
<!-- The HTML for the list of selectable elements -->
Select the products that you're interested in:<br>
<ol id="solutions">
    <li id="vProspect"><img src="images/logo_vprospect.gif"></li>
    <li id="vConvert"><img src="images/logo_vconvert.gif"></li>
    <li id="vRetain"><img src="images/logo_vretain.gif"></li>
</ol>
<p>Product(s) selected: ><span id="selected"></span></p>
```

```javascript
//The jQuery for the interaction
$(document).ready(function() {
    $("#solutions").selectable({
        stop: function() {
            $("#selected").text("");
            //the 'ui-selected' id is a part of jQuery UI
            $(".ui-selected").each(function() {
                $("#selected").append(this.id + " ");
            });
        }
    });
});
```

```html
<!-- The HTML for the sortable list -->
<ul id="vsupport">
    <!-- 'ui-state-default' is part of jQuery UI & sets a baseline style for the items -->
    <li class="ui-state-default">Blog / How-To Articles</li>
    <li class="ui-state-default">Discussion Forum</li>
    <li class="ui-state-default">Knowledge Base</li>
    <li class="ui-state-default">Phone Support</li>
    <li class="ui-state-default">Wiki Support</li>
</ul>
```

```javascript
//The jQuery for the interaction
$(document).ready(function() {
    $("#vsupport").sortable({
        // 'ui-state-highlight' is a part of jQuery UI
        placeholder: "ui-state-highlight"
    });
});
```

## How to Use Effects

jQuery UI Core Effects:

  1. Color Transitions - Provides for animating background color, border colors, text color, and outline color.
  2. Class Transitions - Provides for animations while a class is being added, deleted or changed.
  3. Easing - Provides easing effects to animated elements.
  4. Visibility Transitions - Provides for applying an individual effect to an element while showing, hiding, or toggling the element.

The syntax for the effect method - `effect(effect[, {options}] [, duration] [, callback])`

```html
<!-- The HTML for the sortable list -->
<ul id="vsupport">
    <!-- 'ui-state-default' is part of jQuery UI & sets a baseline style for the items -->
    <li class="ui-state-default">Blog / How-To Articles</li>
    <li class="ui-state-default">Discussion Forum</li>
    <li class="ui-state-default">Knowledge Base</li>
    <li class="ui-state-default">Phone Support</li>
    <li class="ui-state-default">Wiki Support</li>
</ul>
```

```javascript
//The jQuery for the effects
$(document).ready(function() {
    $("#vsupport").sortable({
        // 'ui-state-highlight' is a part of jQuery UI
        placeholder: "ui-state-highlight"
        start: function(event, ui) {
            $(ui.item).effect("pulsate", { times: 3 }, 1500);
        }
        update: function(event, ui) {
            $(ui.item).effect("highlight", { color: "#7fffd4" }, 2000);
        }
    });
});
```

If you code a callback function as a parameter of the effect method, the function is called after the effect is executed.

If you code the effect method with a callback function, the function should accept event and ui parameters. The event parameter contains information about the original browser event, and the ui parameter contains information about the selected item.

```html
<!-- the HTML for the text area and link -->
<textarea id="comments" style="width:350px;height:125px;"></textarea><br>
<a href="#" id="grow_textarea">Increase text area</a>
```

```javascript
//The jQuery for the transition
$(document).ready(function() {
    $("#grow_textarea").click(function() {
        $("#comments").animate({
            width: 500,
            height: 200,
            backgroundColor: "#ededed",
            color: "green"
        }, 1000 );
    });
});
```

The Syntax of the Methods for Class Transitions:

  1. `addClass(className[, duration])`
  2. `removeClass(className[, duration])`
  3. `toggleClass(className[, duration])`
  4. `switchClass(removeName, addName[, duration])`

```html
<!-- The HTML for the class transition -->
Change text size:
<input type="button" id="button1" value="Medium">
<input type="button" id="button2" value="Large">
<input type="button" id="button3" value="X-Large">
<h2>Welcome</h2>
<p id="p1">... INSERT CONTENT HERE ...</p>
```

```javascript
//The jQuery for the class transitions
$(document).ready(function() {
    $("#button1").click(function() { setSize("medium"); });
    $("#button2").click(function() { setSize("large"); });
    $("#button3").click(function() { setSize("x_large"); });

    function setSize(size) {
        $("#p1").removeClass();
        $("#p1").addClass(size, 1000);
    }
});
```

The syntax of the methods for visibility transitions - `{show|hide|toggle} (effect[, {options}] [, duration] [, callback])`

```html
<!-- The HTML for a menu with an item that contains a submenu -->
<ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="aboutus.html">About Us</a></li>
    <li><a href="#" id="solutions">Solutions</a></li>
    <div id="solutions_menu">
        <a href="solutions.html#vprospect">vProspect 2.0</a>
        <a href="solutions.html#vconvert">vConvert 2.0</a>
        <a href="solutions.html#vretain">vRetain 1.0</a>
    </div>
    <li><a href="support.html">Support</a></li>
    <li><a href="contactus.html">Contact Us</a></li>
</ul>
```

```javascript
//The jQuery for the visibility transition
$(document).ready(function() {
    $("#solutions").click(function() {
        $("#solutions_menu").toggle("blind", 500);
    });
});
```

***

### END CHAPTER

Robert Juall

28NOV2016