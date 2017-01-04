# Get Off to a Fast Start with jQuery UI Themes and Widgets

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 313

***

## Introduction to jQuery UI

*jQuery UI* is a free, open-source, Javascript library that extends the use of the jQuery library by providing higher-level features that you can use with a minimum of code.

jQuery UI is available here - `http://jqueryui.com/`

jQuery UI provides four types of features - Themes, Widgets, Interactions, and Effects.

When jQuery UI is downloaded which components are included can be chosen at that time, potentially reducing the size of the download for the user.

Some jQuery UI widgets are similar to HTML5 controls, and care should be taken in their use over the corresponding HTML5 element.

jQuery UI interactions can be applied to any HTML element, i.e. making a `<ul>` sortable or a `<tr>` selectable.

jQuery UI effects can be used with interactions, widgets, or HTML5 elements.

jQuery UI Components: 

  1. Core Components
      1. Core - Provides the core functionality. It is required for all interactions and widgets.
      2. Widget - Provides the base functionality for all widgets.
      3. Mouse - Provides the base functionality for all interactions that require the mouse.
      4. Position - Required for all interactions that require the positioning of elements.
  2. Widgets
      1. Accordion - An accordion.
      2. Autocomplete - A text box that displays a list of suggested items based on the user entries.
      3. Button - A customizable button.
      4. Datepicker - A calendar that can be toggled from a textbox or displayed inline.
      5. Dialog - A modal dialog box that is resizable and draggable.
      6. Menu - A menu that can include submenus.
      7. Progressbar - A status indicator that can be used to display progress or percentage values.
      8. SelectMenu - A list box or drop-down list that's customizable and themeable.
      9. Slider - A slider that can display a range of values.
      10. Spinner - A text box with up and down arrows for increasing or decreasing the number.
      11. Tabs - A set of tabs that reveals a tab's contents when the tab is clicked.
      12. Tooltip - A tooltip that's customizable and themeable.
  3. Interactions
      1. Draggable - Makes an element on a web page draggable.
      2. Droppable - Defines targets that draggable objects can be dropped within.
      3. Resizable - Makes an element on a web page resizable.
      4. Selectable - Makes an element selectable with a mouse.
      5. Sortable - Makes a list of items sortable.
  4. Effects
      1. Effects Core - Required for all effects.
      2. Blind - Creates a blind effect similar to vertical blinds on a window.
      3. Bounce - Bounces an element up and down or side to side.
      4. Clip - Clips the element on and off.
      5. Drop - Moves an element in one direction and hides it at the same time.
      6. Explode - Explodes and element in all directions. Also supports imploding.
      7. Fade - Fades the element in or out.
      8. Fold - Folds an element horizontally and then vertically.
      9. Highlight - Highlights an element's background with a color for a specified length of time.
      10. Puff - Grows and hides or shrinks and shows an element
      11. Pulsate - Pulsates an element for a certain amount of time by changing the opacity.
      12. Scale - Grows or shrinks an element and its content.
      13. Shake - Shakes an element up and down or side to side for a specified amount of time.
      14. Size - Changes the size of an element to the specified width and length.
      15. Slide - Slides an element in and out of the screen.
      16. Transfer - Transfers an element from one element to another.

## How to Build and Use a jQuery UI Download

If all options are selected, the jQuery UI library is roughly 200kb.

If 'design a custom theme' is selected, ThemeRoller will be loaded.

ThemeRoller is a GUI tool that allows for the customization of jQuery UI elements.

A theme is not required, a css style sheet can be used to change the look of jQuery UI elements.

The jQuery UI download includes many files, some of which need to be linked to in a HTML document in order to be utilized.

## How to Use jQuery UI Widgets

```javascript
//The jQuery for using a widget
$(document).ready(function() {
    $("selector").widgetMethod({
        // option settings
    });
});
```

For a widget that requires images, jQuery UI expects the css file and the images folder to be at the same level.

The jQuery UI documentation provides information regarding all of the options, etc. for each widget.

The accordion widget consists of `<h3>` elements that provide the headers for the panels, followed by `<div>` elements that contain the contents for the panels, these elements should be within an outer `<div>` element that represents the accordion.

```html
<!-- The HTML for the accordion -->
<div id="accordion">
    <h3>What is jQuery?</h3>
    <div>
        <!-- the content for the panel -->
    </div>
    <h3>Why is jQuery becoming so popular?</h3>
    <div>
        <!-- the content for the panel -->
    </div>
    <h3>Which is harder to learn: jQuery or Javascript?</h3>
    <div>
        <!-- the content for the panel -->
    </div>
</div>
```

```javascript
//The jQuery for the accordion
$(document).ready(function() {
    $("accordion").accordion({
        event: "mouseover",
        collapsible: true
    });
});
```

```html
<div id="tabs">
    <ul>
        <li><a href="#tabs-1">Book description</a></li>
        <li><a href="#tabs-2">About the authors</a></li>
        <li><a href="#tabs-3">Who this book is for</a></li>
    </ul>
    <div id="tabs-1"><!-- the content --></div>
    <div id="tabs-2"><!-- the content --></div>
    <div id="tabs-3"><!-- the content --></div>
</div>
```

```javascript
//The jQuery for tabs
$(document).ready(function() {
    $("#tabs").tabs();
});
```

The jQuery UI 'button' widget works with HTML button, submit, reset, radio, checkbox, and `<a>`

The 'dialog' widget is considered to be a nice improvement over the Javascript technique for opening another window and using it as a dialog box, especially because most browsers have built-in features for blocking popups.

```html
<!-- The HTML for the Button and Dialog widgets -->
<a id="book"><img src="images/html5.jpg" alt="HTML5 and CSS3 book"
    width="150" height="188" /></a>
<div id="dialog" title="HTML5 and CSS3" style="display:none;">
    <!-- the content for the dialog box -->
</div>
```

```javascript
//The jQuery for the Button and Dialog widgets
$(document).ready(function() {
    $("#book").button():
    $("#book").click(function() {
        $("#dialog").dialog({ modal: true });
    });
});
```

```html
<!-- The HTML for the Autocomplete widget -->
<div class="ui-widget">
    <label for="books">Book: </label>
    <input id="books">
</div>
```

```javascript
//The jQuery for the Autocomplete widget
$(document).ready(function() {
    var murachBooks = 
        ["ADO.NET", "Android", "ASP.NET", "C#", "C++", "CSS",
         "Dreamweaver CC", "HTML5", "Java", "Java Servlets",
         "Javascript", "jQuery", "MySQL", "Oracle SQL", "PHP",
         "SQL Server", "VB", "Web Development", "Web Programming"];
    $("#books").autocomplete({
        source: murachBooks
    });
});
```

```html
<!-- The HTML for the Slider widget -->
<div id="size">
    <label>Company size: </label>
    <input type="text" id="employees" style="border:0;">
</div>
<div id="slider" style="width:100px;"></div>
```

```javascript
//The jQuery for the Slider widget
$(document).ready(function() {
    $("#slider").slider({
        value: 50,
        min: 1,
        max: 100,
        slide: function(event, ui) {
            $("#employees").val(ui.value);
        }
    });
    $("employees").val(50);
});
```

```html
<!-- The HTML for the Menu widget -->
<ul id="menu">
    <li><a href="index.html">Home</a></li>
    <li><a href="aboutus.html">About Us</a>
        <ul>
            <li><a href="history.html">Company History</a></li>
            <li><a href="staff.html">Our Staff</a></li>
            <li><a href="headquarters.html">Our Headquarters</a></li>
        </ul>
    </li>
    <li><a href="solutions.html">Solutions</a>
        <ul>
            <li><a href="vProspect.html">vProspect 2.0</a></li>
            <li><a href="vConvert.html">vConvert 2.0</a></li>
            <li><a href="vRetain.html">vRetain 1.0</a></li>
        </ul>
    </li>
    <li><a href="support.html">Support</a></li>
    <li><a href="contactus.html">Contact Us</a></li>
</ul>
```

```javascript
//The jQuery for activating the Menu widget
$(document).ready(function() {
    $("#menu").menu({
        icons: { submenu: "ui-icon-triangle-1-e" }
    });
});
```

## A Web Page that Uses jQuery UI

```html
<!-- The HTML for the widgets -->
<form id="contactusForm">
    <p>Fill out the form below and a sales representative will contact you shortly. For more information on how to fill out this form, please review our <a href="#" id="help">vSupport documentation</a>.</p>

    <!-- DIALOG WIDGET -->
    <div id="helpdialog" title="vSupport" style="display:none;">
        <p>Our contact form is divided into four sections: ... </p>
    </div>

    <!-- TABS WIDGET -->
    <div id="tabs">
        <ul>
            <li><a href="#tabs-1">Personal</a></li>
            <li><a href="#tabs-2">Company</a></li>
            <li><a href="#tabs-3">Product</a></li>
            <li><a href="#tabs-4">Additional</a></li>
        </ul>
        <div id="tabs-1">
            .
            .
        </div>
        <div id="tabs-2">
            .
            .
            <label>Company Size:</label>
            <input type="text" id="employees" style="border:0;">
            <!-- SLIDER WIDGET -->
            <div id="slider"></div><br>
            .
            .
        </div>
        <div id="tabs-3">
            .
            .
        </div>
        <div id="tabs-4">
            .
            .
            <!-- DATEPICKER WIDGET -->
            <input type="text" id="datepicker"><br>
        </div>
    </div>
    <!--BUTTON WIDGET -->
    <input type="submit" id="submitbutton" value="Submit Form">
</form>
```

```javascript
//The jQuery for the widgets
$(document).ready(function() {
    //DIALOG WIDGET
    $("help").click(function() {
        buttons: {
            OK: function() {
                $(this).dialog("close");
            }
        }
    });

    //TABS WIDGET
    $("#tabs").tabs();

    //SLIDER WIDGET
    $("#slider").slider({
        min: 1,
        max: 100,
        range: true,
        values: [11, 50],
        slide: function(event, ui) {
            $("#employees").val(ui.values[0] + " - " + ui.values[i]);
        }
    });
    $("#employees").val(11 + " - " + 50);

    //DATEPICKER WIDGET
    $("#datepicker").datepicker();

    //BUTTON WIDGET
    $("#submitbutton").button();
});
```

***

### END CHAPTER

Robert Juall

28NOV2016