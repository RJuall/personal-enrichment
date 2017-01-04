# How to Create and Use jQuery Plugins

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 223

***

## Introduction to Plugins

A *jQuery plugin* is a javascript application that does one web task or set of related web tasks and uses the jQuery library

Common websites for finding jQuery plugins:

  1. jQuery Plugin Repository - plugins.jquery.com
  2. jQuery Plugins - jquery-plugins.net
  3. Google Code - code.google.com
  4. GitHub - github.com
  5. Sourceforge - sourceforge.net

Plugins can save a lot of development time

Some of the most useful jQuery plugins:

  1. Lightbox (images)
  2. Fancybox (images)
  3. Thickbox (images)
  4. Colorbox (images)
  5. bxSlider (gallery)
  6. Malsup jQuery Cycle 3 (gallery)
  7. jCarousel (gallery)
  8. Galleria (gallery)
  9. UI Layout (Layout)
  10. Masonry (Layout)
  11. Columnizer (Layout)
  12. jsColumns (Layout)
  13. jLayout (Layout)
  14. Malsup jQuery Form (Forms)
  15. Ideal Forms (Forms)
  16. jQuery Validation (Forms)
  17. jqTransform (Forms)
  18. jQuery UI (Interface)
  19. Isotope (Interface)
  20. WOW (Interface)
  21. Wijmo (Interface)
  22. jQuery Mobile (Mobile)

Plugins may include CSS, javascript, images, or other files

Files such as CSS and javascript must be linked to in the html document

Some plugins may require a specific version of jQuery

It's important to read the documentation for plugins to understand their use, etc.

## How to Use Three of the Most Useful Plugins

The *Lightbox* plugin displays a larger version of a thumbnail image when the user clicks on the thumbnail image, displayed in a modal box.

Lightbox requires both CSS, image, and javascript files

*bxSlider* is a plugin used to create carousels, it also has both CSS, image, and javascript files

Much can be learned from reading and/or adjusting the CSS files used by plugins

The *Cycle 2* plugin is used to create slide shows, it only requires a javascript file

## How to Create Your Own Plugins

jQuery provides an *API (Application Programming Interface)* that allows a programmer to create plugins

Before creating a plugin, make sure that it is truly needed

Creating plugins is a lengthy process that takes time to mature

A plugin function is wrapped within an *Immediately Invoked Function Expression (IIFE)*

It is coded in this way to prevent conflicts with the `$` marker, other plugins, jQuery, etc.

The API Standards for Plugins:

  1. The plugin should support implicit iteration
  2. The plugin should preserve chaining by returning the selected object
  3. The plugin definitions should end with a semicolon
  4. The plugin options should provide reasonable defaults
  5. The plugin should be well-documented

For many plugins, most of the code will be in the function of the each method

When the function finishes, the `this` object should be returned to the calling application

```javascript
//A simple selection plugin
(function($) {
    $.fn.displaySelection = function() {
        return this.each(function() {
            alert("The text for the selection is '" + $(this).text() + "'");
        })
    }
}) (jQuery);

//The jQuery for using this plugin
$(document).ready(function() {
    $("#faqs h2").displaySelection();
});
```

naming conventions for plugin files - `jquery.pluginName.js`

To support 'implicit iteration' use the `each` method within the plugin function

To preserve chaining return the `this` object

```javascript
//A jQuery plugin that highlights
(function($) {
    $.fn.highlightMenu = function() {
        return this.each(function() {
            var items = $("li a");
            items.css('font-family', 'arial, helvetica, sans-serif')
                 .css('font-weight', 'bold')
                 .css('text-decoration', 'none')
                 .css('background-color', '#dfe3e6')
                 .css('color', '#cc1c0d')
                 .css('width', '125px');
            items.mouseover(function() {
                $(this).css('background-color', '#000')
                       .css('color', '#fff');
            });
            items.mouseout(function() {
                $(this).css('background-color', '#dfe3e6')
                       .css('color', '#cc1c0d');
            });
        });
    }
}) (jQuery);
```

To make a plugin more useful, options can be provided

There should always be defaults for any options provided

```javascript
//Highlight menu with options
(function($) {
    $.fn.highlightMenu = function(options) {
        var defaults = $.extend({
            'bgcolor'       : '#000000',
            'color'         : '#ffffff',
            'hoverBgColor'  : '#cccccc',
            'hoverColor'    : '#000000',
            'linkWidth'     : '125px',
        }, options);

        return this.each(function() {
            var items = $("li a ");
            var o = defaults;

            items.css('font-family', 'arial, helvetica, sans-serif')
                 .css('font-weight', 'bold')
                 .css('text-decoration', 'none')
                 .css('background-color', o.bgColor)
                 .css('color', o.color)
                 .css('width', o.linkWidth);

            items.mouseover(function() {
                $(this).css('background-color', o.hoverBgColor)
                       .css('color', o.hoverColor);
            });

            items.mouseout(function() {
                $(this).css('background-color', o.bgColor)
                       .css('color', o.color);
            });
        });
    }
}) (jQuery);
```

To set default options, use the `$.extend` method, which creates an object from the name/value pairs in its first parameter. Then it merges those pairs with the name/value pars in its second parameter, which are the options set by the user.

## A Web Page That Uses Two Plugins

***

### END CHAPTER

Robert Juall

14NOV2016