# How to Work With Forms and Data Validation

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 249

***

## Introduction to Forms and Controls

A *form* contains one or more *controls* such as text boxes and buttons.

The controls that accept user entries are also known as *fields*

The data submitted using the HTTP GET method is visible in the browser address bar & can be bookmarked

The data submitted using the HTTP POST method is not visible to the user & is much more secure

The *submit button* is the control that sends data collected by the form to the server

The *reset button* sets the values of all the form controls to their default values

*Data validation* is the process of making sure that data submitted as part of a form is appropriate to their types, etc.

Some data validation is usually done on the client side and some is done on the server side

Common HTML5 controls for input data:

  1. `email` - Gets an email address with validation done by the browser.
  2. `url` - Gets a URL with validation done by the browser.
  3. `tel` - Gets a telephone number with no validation done by the browser.
  4. `number` - When supported, gets a numeric entry with min, max, and step attributes, browser validation, and up and down arrows.
  5. `range` - When supported, gets a numeric entry with min, max, and step attributs, browser validation, and a slider control.
  6. `date` - When supported, gets a date entry with min and max attributes and may include a popup calendar or up and down arrows.
  7. `time` - When supported, gets a time entry with min and max attributes and may include up and down arrows.

The basic HTML5 attributes for working with forms:

  1. `autofocus` - A boolean attribute that tells the browser to set the focus on the field when the page is loaded.
  2. `placeholder` - A message in the field that is removed when the contol receives the focus.

Many of the HTML5 input controls provide for basic data validation. You can also use the HTML5 attributes in figure 8-3 for data validation.

The HTML5 attributes for data validation:

  1. `required` - A boolean attribute that indicates that a value is required for a field.
  2. `title` - Text that is displayed in a tooltip when the mouse hovers over a field. This text is also displayed after teh browser's default error message.
  3. `pattern` - A regular expression that is used to validate the entry in a field.
  4. `novalidate` - A boolean attribute that tells the browser that it shouldn't validate the form or control that it is coded for.
  5. `autocomplete` - Set this attribute to off to tell the browser to disable auto-completion. This can be coded for a form or a control.

A *regular expression* provides a way to match a user entry against a *pattern* of characters, used mainly for data validation.

*Auto-completion* is a modern feature that provides suggestions to a user filling out a form. Turned on by default.

Javascript is needed for data validation because browsers may not implement all of the HTML5 validation features and the HTML5 features are limited in their abilities.

## How to Use jQuery to Work With Forms

The jQuery selectors for form controls:

  1.  `:input` - All input, select, textarea, and button elements.
  2.  `:text` - All text boxes: input elements with type equal to 'text'.
  3.  `:radio` - All radio buttons: input elements with type equal to 'radio'.
  4.  `:checkbox` - All check boxes: input elements with type equal to 'checkbox'.
  5.  `:file` - All file upload fields: input elements with type equal to 'file'.
  6.  `:password` - All password fields: input elements with type equal to 'password'.
  7.  `:submit` - All submit buttons and button elements: input elements with type equal to 'submit' and button elements.
  8.  `:reset` - All reset buttons: input elements with type equal to 'reset'.
  9.  `:image` - All image buttons: input elements with type equal to 'image'.
  10. `:button` - All buttons: button elements and input elements with type equal to 'button'.
  11. `:disabled` - All disabled elements: elements that have the disabled attribute.
  12. `:enabled` - All enabled elements: elements that don't have the disabled attribute.
  13. `:checked` - All check boxes and radio buttions that are checked.
  14. `:selected` - All options in select elements that are selected.

jQuery methods for getting and setting control values - `val()` (gets a value), `val(value)` (sets a value).

jQuery method for trimming an entry - `string.trim()`

jQuery event methods for forms:

  1. `focus(handler)` - The handler runs when the focus moves to the selected element.
  2. `blur(handler)` - The handler runs when the focus leaves the selected element.
  3. `change(handler)` - The handler runs when the value in the selected element is changed.
  4. `select(handler)` - The handler runs when the user selects text in a text or textarea box.
  5. `submit(handler)` - The handler runs when a submit button is clicked.

jQuery methods for triggering events:

  1. `focus()` - moves the focus to the selected element and triggers the focus event.
  2. `blur()` - Removes the focus from the selected element and triggers the blur event.
  3. `change()` - Triggers the change event.
  4. `select()` - Triggers the select event.
  5. `submit()` - Triggers the submit event for a form.

```javascript
//A handler that disables or enables radio buttons
//when a check box is checked or unchecked
$("#contact_me").change(        // the change event for a check box
    function() {
        if ($("#contact_me").attr("checked")) {
            $(":radeo").attr("disabled", false) //enables radio buttons
        }
        else {
            $(":radio").attr("disabled", true) //disables radio buttons
        }
});
```

An event handler for the click event of a regular button (not a submit button) can be used to validate the data in a form, once the data passes validation then the submit method can be called.

## A Validation Application that Uses Javascript

```javascript
$(document).ready(function() {
    // add span element after each input element
    $(":text, :password").after("<span>*</span>");

    // put today's date in the start_date text box
    var today = new Date();
    var month = today.getMonth() + 1;   // Add 1 since months start at 0
    var day = today.getDate();
    var year = today.getFullYear();
    var dateText = ((month < 10) ? "0" + month : month) + "/";  // pad month
    dateText += ((day < 10) ? "0" + day : day) + "/";           // pad date
    dateText += year;
    $("start_date").val(dateText);

    $("#member_form").submit(
        function(event) {
            var isValid = true;

            // validate the email entry with a regular expression
            var emailPattern =
                /\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}\b/;
            var email = $("#email").val();
            if (email == "") {
                $("#email").next().text("This field is required.");
                isValid = false;
            } else if (!emailPattern.test(email)) {
                $("#email").next().text("Must be a valid email address.");
                isValid = false;
            } else {
                $("#email").next().text("");
            }

            // validate the password entry
            var password = $("#password").val();
            if (password.length < 6) {
                $("#password").next().text("Must be 6 or more characters");
                isValid = false;
            } else {
                $("#password").next().text("");
            }

            // validate the first name entry
            var firstName = $("#first_name").val().trim();
            if (firstName == "") {
                $("#first_name").next().text("This field is required.");
                isValid = false;
            } else {
                $("#first_name").val(firstName);
                $("#first_name").next.text("");
            }

            // prevent the submission of the form if any entries are invalid
            if (isValid == false) { event.preventDefault(); }
        }   // end function
    )       // end submit
});         // end ready
```

## How to Use a Plugin for Data Validation

```javascript
//The javascript that uses the validate method of the plugin
//http://jqueryvalidation.org
$("#email_form").validate({     //use the id attribute to select the form
    rules: {
        email_address: {        //use the name attributes to refer to fields
            required: true,
            email: true
        },
        first_name: {
            required: true
        }
    },
    messages: {
        email_address: {        //use the name attributes to refer to fields
            required: "Please supply an email address.",
            email: "This is not a valid email address."
        },
        first_name: {
            required: "Please supply a first name."
        }
    }
});     //end validate
```

The validation options for the validate method of the plugin:

  1. `required: true` - This field is required.
  2. `email: true` - Please enter a valid email address.
  3. `url: true` - Please enter a valid URL.
  4. `date: true` - Please enter a valid date.
  5. `dateISO: true` - Please enter a valid date (ISO).
  6. `number: true` - Please enter a valid number.
  7. `digits: true` - Please enter only digits.
  8. `creditcard: true` - Please enter a valid credit card number.
  9. `equalTo: "selector"` - Please enter the same value again.
  10. `maxlength: value` - Please enter no more than (value) characters.
  11. `minlength: value` - Please enter at least (value) characters.
  12. `rangelength: [value1, value2]` - Please enter a value between (value1) and (value2) characters long.
  13. `max: value` - Please enter a value less than or equal to (value).
  14. `min: value` - Please enter a value greater than or equal to (value).
  15. `range: [value1, value2]` - Please enter a value between (value1) and (value2).

When the validate method finds an error it inserts a label element into the DOM right after the input element that has the invalid data. This label displays the error message and is removed from the DOM when the error is corrected.

The plugin's error messages can be formatted referencing the class 'error'

## A Validation Application that Uses the Validation Plugin

```javascript
//The jQuery for a validation application using the plugin
$(document).ready(function() {
    $("#email").focus();

    //other setup processing can go here

    $("#member_form").validate({
        rules: {
            email: {
                required: true,
                email: true
            },
            password: {
                required: true,
                minlength: 6
            },
            verify: {
                required: true,
                equalTo: "#password"
            },
            first_name: {
                required: true
            },
            last_name: {
                required: true
            },
            state: {
                required: true,
                rangelength: [2, 2]
            },
            zip: {
                required: true,
                rangelength: [5, 10]
            },
            phone: {
                required: true,
                phoneUS: true
            },
            start_date: {
                required: true,
                date: true
            },
            card_number: {
                required: true,
                creditcard: true
            }
        }
    });     //end validate
});         //end ready
```

***

### END CHAPTER

Robert Juall

20NOV2016