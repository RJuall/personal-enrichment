# How to Enhance a jQuery Mobile Website

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 507

***

## How to Use the jQuery Mobile Documentation

For information about jQuery Mobile components, functions, etc. look at the jQuery Mobile documentation.

## How to Use jQuery Mobile to Format Content

```html
<!-- HTML for 2 columns in jQuery Mobile -->
<section class="ui-grid-a">
  <div class="ui-block-a">
    <img src="images/agnes.gif" alt="Agnes">
    <h4><a href="#agnes">Agnes Agnew</a></h4>
    <p>VP of Accounting</p>
    <!-- the code for the other speakers in the first column -->
  </div>
  <div class="ui-block-b">
    <img src="images/mike.gif" alt="Mike">
    <h4><a href="#mike">Mike Masters</a></h4>
    <p>VP of Marketing</p>
    <!-- the code for the other speakers in the second column -->
  </div>
</section>
```

A *collapsible content block* is similar to an accordion, but more than one section can be displayed at a time.

```html
<!-- HTML for collapsible content blocks in jQuery Mobile -->
<div data-role="collapsible">
  <h3>Agnes Agnew</h3>
  <img src="images/agnes.gif" alt="Agnes">
  <h4>Agnes Agnew<br>VP of Accounting</h4>
  <p>With over 14 years of public accounting and business...</p>
</div>
<div data-role="collapsible" data-collapsed="false">
  <h3>Mike Masters</h3>
  <img src="images/mike.gif" alt="Mike">
  <h4>Mike Masters<br>VP of Marketing</h4>
  <p>Mike serves as the Vice President of Sales and Marketing...</p>
</div>
<!-- the div elements for the other content blocks -->
```

jQuery Mobile automatically adds the plus/minus icons to collapsible content blocks - the icons can be changed.

*Collapsible sets* are similar to collapsible content blocks except that only one can be displayed at a time.

```html
<section data-role="collapsibleset">
  <div data-role="collapsible" data-collapsed="false">
    <h3>Agnes Agnew</h3>
    <!-- ETC. -->
```

## How to Use jQuery Mobile for List Views

A *list view* consists of a list of items that link to other pages.

```html
<!-- HTML for a list view, jQuery Mobile -->
<ul data-role="listview">
  <li><a href="#agnes">Agnes Agnew</a></li>
  <li><a href="#mike">Mike Masters</a></li>
  <!-- ETC. -->
```

jQuery Mobile automatically adds the right arrow icon to list view items, which can be changed.

Transition effects can be added to list view links.

*Split button lists* let one divide each list item into two tappable areas.

*Inset lists* are typically used when a page has content other than the list and is an element on a page, rather than the page itself.

Inset list - `<ul data-role="listview" data-split-icon="gear" data-inset="true">`

```html
<!-- Split Button List -->
<ul data-role="listview">
  <li>
    <a href="#agnes">
      <img src="images/agnes.gif" alt="Agnes">
      <h3>Agnes Agnew</h3>
      <p>VP of Accounting</p>
    </a>
    <a href="mailto:agnes@vectacorp.com" title="Send Email">
      Send Email</a>
  </li>
  <!-- Other list items -->
</ul>
```

*List dividers* are used to group list items together.

```html
<!-- List Dividers -->
<ul data-role="listview">
  <li data-role="list-divider">Executives</li>
  <li><a href="#agnes">Agnes Agnew</a></li>
  <!-- ETC. -->
  <li data-role="list-divider">Managers</li>
  <li><a href="#wally">Wally Waters</a></li>
  <!-- ETC. -->
```

*Count bubbles* provide a way of displaying the number of items in a list item that represent a group.

```html
<!-- Content Bubbles -->
<ul data-role="listview">
  <li><a href="#emps">Executives<span class="ui-li-count">5</span></a></li>
  <li><a href="#mgrs">Managers<span class="ui-li-count">25</span></a></li>
  <!-- ETC. -->
```

## How to Use jQuery Mobile for Forms

All of the jQuery Mobile form controls are enhanced versions of the standard HTML form controls.

```html
<!-- The HTML for the text fields and text area -->
<label for "name">Name:</label>
<input type="text" name="name" id="name">
<label for="companyname">Company Name:</label>
<input type="text" name="companyname" id="companyname">
<label for="phone">Phone:</label>
<input type="tel" name="phone" id="phone">
<label for="email">Email:</label>
<input type="email" name="email" id="email">
<label for="questions">Questions/Comments:</label>
<textarea name="questions" id="questions"></textarea>
```

```html
<!-- The HTML for the slider and switch -->
<label for="size">Company Size:</label>
<input type="range" name="size" id="size" min="10" max="500" value="300"
  setp="10" data-highlight="true"><br>
<label for="currentinstall">Currently Installed vSolutions?</label>
<select name="currentinstall" id="currentinstall" data-role="flipswitch">
  <option value="No">No</option>
  <option value="Yes">Yes</option>
</select>
```

```html
<!-- The HTML for the check box and radio button -->
<fieldset data-role="controlgroup">
  <legend>Which solutions are you interested in?</legend>
  <input type="checkbox" name="vprospect" id="vprospect">
  <label for="vprospect">vProspect</label>
  <!-- ETC. -->
</fieldset>
<fieldset data-role="controlgroup" data-type="horizontal">
  <legend>Current infrastructure?</legend>
  <input type="radio" name="infrastructure" id="linux">
  <label for="linux">Linux</label>
  <input type="radio" name="infrastructure" id="mac">
  <label for="mac">Mac</label>
  <!-- ETC. -->
</fieldset>
```

```html
<!-- The HTML for the select menu -->
<label for="hearaboutus">How did you hear about us?</label>
<select name="hearaboutus" id="hearaboutus">
  <option value="magazine">Magazine Ad</option>
  <option value="radio">Radio Ad</option>
  <option value="tv">TV Ad</option>
  <option value="word">Word of Mouth</option>
</select>
```

When a select menu is tapped, the mobile browser will display the phone's roulette with the list of items.

By default a jQuery Mobile form is submitted using Ajax, which can be changed.

```html
<!-- The HTML for the form and submit button -->
<form action="../scripts/mobile.asp" method="post" data-ajax="false">
  
  <!-- Mobile form elements go here -->
  
  <input type="submit" value="Submit Form">
</form>
```

## An Enhanced Mobile Website for Vecta Corp

...

***

### END CHAPTER

Robert Juall

05DEC2016