# Get Off to a Fast Start with jQuery Mobile

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 469

***

## How to Work with Mobile Devices

jQuery can be used to redirect mobile browsers to a different version of a site

Mobile sites are, by convention, preceded by an `m` as in `m.google.com`

Though jQuery can be used in this way, it is preferred to use *responsive web design* instead, building the HTML/CSS in a such a way to look good on many different screen sizes

Responsive web design involves using *fluid layouts*, *scalable images*, and *media queries*

Converting a large-scale website from a static layout to a responsive one can be time-consuming and expensive.

The easiest way to get started with browser/mobile detection in Javascript/jQuery is to use a plugin such as `detectmobilebrowser`

Basic *viewport* settings for a mobile website - `<meta name="viewport" content="width=device-width, initial-scale=1">`

Basic viewport settings for a full website - `<meta name="viewport" content="width=device-width, initial-scale=.5">`

Content properties for viewport metadata:

  1. `width` - The width of the viewport in pixels. You can also use the device-width keyword to indicate that the viewport should be as wide as the screen.
  2. `height` - The height of the viewport in pixels. You can also use the device-height keyword to indicate that the viewport should be as tall as the screen.
  3. `initial-scale` - A number that indicates the initial zoom factor that's used to display the page.
  4. `minimum-scale` - A number that indicates the minimum zoom factor for the page.
  5. `maximum-scale` - A number that indicates the maximum zoom factor for the page.
  6. `user-scalable` - Indicates whether the user can zoom in and out of the viewport.

Guidelines for designing mobile web pages:

  1. Keep your layout simple so the focus is on the content. One-column layouts typically work best.
  2. Include only essential content.
  3. Keep images small and to a minimum.
  4. Avoid using Flash. Most mobile devices, including the iPhone, don't support it.
  5. Include only the essential navigation in the header of the page. The other navigation should be part of the content for the page.
  6. Make links and other elements large enough that the user can easily manipulate them.
  7. Use relative measurements so the page looks good regardless of the scale.

Guidelines for testing mobile web pages:

  1. Test all pages on as many different mobile devices and in as many different mobile browsers as possible.
  2. The best way to test mobile web pages is to deploy them to your web server and test them on the devices themselves.
  3. When you can't test your pages on the devices themselves, you can use web-based tools such as ProtoFluid, device emulators and browser simulators, or the developer tools that come with Chrome, Firefox, and IE.

## How to Get Started with jQuery Mobile

*jQuery Mobile* is a free, open-source, cross-platform, Javascript library tht one can use for developing mobile websites.

The jQuery mobile library requires the core jQuery library and the jQuery Mobile CSS file in order to work.

jQuery Mobile lets one store multiple pages in a single HTML file; create dialogs, buttons, and navigation bars; format pages without coding CSS; lay out pages with two columns, collapsible content blocks, and accordions, etc.

```html
<!-- The HTML for a jQuery Mobile web page -->
<div data-role="page">
  <header data-role="header">
    <h1>Header</h1>
  </header>

  <section class="ui-content" role="main">
    <p>The page content</p>
  </section>

  <footer data-role="footer">
    <h4>Footer</h4>
  </footer>
</div>
```

jQuery Mobile allows one to create multiple pages in a single HTML file by coding each web page into a `div` with a unique id.

HTML that causes a page to open as a dialog - `<div data-role="page" id="vprospect" data-dialog="true">`

HTML that opens the page with the 'pop' transition - `<a href="#vprospect" data-transition="pop">`

To add a button to a web page, code an `<a>` element with its data-role attribute set to 'button'

```html
<!-- The HTML for the buttons in the main content -->
<!-- For inline buttons, set the data-inline attribute to true -->
<a href="#" data-role="button" data-inline="true">Cancel</a>
<a href="#" data-role="button" data-inline="true">OK</a>
<!-- To add an icon to a button, use the data-icon attribute -->
<a href="#" data-role="button" data-icon="delete">Delete</a>
<a href="#" data-role="button" data-icon="home">Home</a>
<!-- To group buttons, use a div element with the attributes that follow -->
<div data-role="controlgroup" data-type="horizontal">
  <a href="#" data-role="button">Yes</a>
  <a href="#" data-role="button">No</a>
  <a href="#" data-role="button">Maybe</a>
</div>
<!-- To code a back button, set the data-rel attribute to back -->
<a href="#" data-role="button" data-rel="back" data-icon="back">
  Back to previous page</a>

<!-- The HTML for the buttons in the footer -->
<footer data-role="footer" class="ui-bar">
  <a href="http://www.facebook.com" data-role="button"
     data-icon="plus">Add to Facebook</a>
  <a href="http://www.twitter.com" data-role="button"
     data-icon="plus">Tweet Page</a>
</footer>
```

To create a navigation bar, code a div element with its data-role attribute set to 'navbar' and code a ul element within it containing the navigation links.

## How to Format Content with jQuery Mobile

jQuery Mobile applies styles to elements that are similar to a mobile device's default styles, this is describes as its default *theme*

jQuery Mobile's default theme comes with two color *swatches*, or colorizations.

A swatch applied to an element will be inherited by all its child elements.

jQuery Mobile also has a diy theme builder online, ThemeRoller.

## A Mobile Website for Vecta Corp

...

***

### END CHAPTER

Robert Juall

05DEC2016