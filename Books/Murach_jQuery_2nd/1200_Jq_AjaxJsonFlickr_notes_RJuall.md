# How to Use Ajax, JSON, and Flickr

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 375

***

## Introduction to Ajax

*Ajax* stands for *Asynchronous Javascript and XML* and is a technology that allows a web page to receive data from a web server without refreshing a web page, also known as a *partial page refresh*

Browsers provide an *XMLHttpRequest object* (*XHR object*) that is used to send Ajax requests to the web server and to receive the returned data from the server. 

The XHR object is handled by Javascript, which issues, parses, and implements the Ajax request.

*APIs* or *Application Programming Interfaces* are rules implemented that describe how a program can be interacted with and utilized.

Three common data formats for Ajax applications - HTML, XML, and JSON.

Other Ajax compatable data formats include TXT, YAML, and CSV.

*XML* stands for *eXtensible Markup Language* and is an open-standard, device independent format for exchanging data over the internet.

XML has syntax and structure similar to HTML.

XML is relatively difficult to parse using Javascript.

*JSON* stands for *Javascript Object Notation* is based on a subset of the Javascript programming language, is "C-style", and is formatted and returned as a Javascript object.

JSON is easily parsed with Javascript.

```xml
<?xml version="1.0" encoding="utf-8"?>
<management>
  <teammember>
    <name>Agnes</name>
    <title>Vice President of Accounting</title>
    <bio>With over 14 years of public accounting... </bio>
  </teammember>
  <teammember>
    <name>Wilbur</name>
    <title>Founder and CEO</title>
    <bio>While Wilbur is the founder and CEO... </bio>
  </teammember>
</management>
```

```json
{"teammembers":[
    {
        "name":"Agnes",
        "title":"Vice President of Accounting",
        "bio":"With over 14 years of public accounting... "
    },
    {
        "name":"Wilbur",
        "title":"Founder and CEO",
        "bio":"While Wilbur is the founder and CEO... "
    }
]}
```

For more information about JSON APIs and support - `www.json.org`

Members of the `XMLHttpRequest` object:

Methods of the `XMLHttpRequest` object:

  1. `abort()` - Cancels the current request.
  2. `getAllResponseHeaders()` - Returns a string that contains the names and values of all response headers.
  3. `getResponseHeader(name)` - Returns the value of a specific response header.
  4. `open(method, url[, async][, user][, pass])` - Opens a connection for a request. The parameters let you set the method to GET or POST, set the URL for the request, set asynchronous mode to true or false, and supply a username and password if authentication is required. When asynchronous mode is used, the application continues while the request is being processed.
  5. `send([data])` - Starts the request. This method must be called after a request connection has been opened.
  6. `setRequestHeader(name, value)` - Specifies a name and value for a request header.

Properties of the `XMLHttpRequest` object:

  1. `readyState` - A numeric value that indicates the state of the current request: 0 is UNSENT, 1 is OPENED, 2 is HEADERS_RECEIVED, 3 is LOADING, and 4 is DONE.
  2. `responseText` - The content that's returned from the server in plain text format.
  3. `responseXml` - The content that's returned from the server in XML format.
  4. `status` - The status code returned from the server in numeric format. Common values include 200 for success and 404 for not found.
  5. `statusText` - The status message returned from the server in text format.

Event of the `XMLHttpRequest` object: `onreadystatechange` - An event that occurs when the state of the request changes.

The two methods that are used with every request are the `open` and `send` methods.

```javascript
// Javascript for getting and parsing XML data
$(document).ready(function() {
    var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status == 200) {
            xmlDoc = xhr.responseXML;
            var team = xmlDoc.getElementsByTagName("teammember");
            var html = "";
            for (i = 0; i < team.length; i++) {
                html +=
                    xmlDoc.getElementsByTagName("name")[i]
                        .childNodes[0].nodeValue + "<br>" +
                    xmlDoc.getElementsByTagName("title")[i]
                        .childNodes[0].nodeValue + "<br>" +
                    xmlDoc.getElementsByTagName("bio")[i]
                        .childNodes[0].nodeValue + "<br><br>";
            }
            document.getElementById("team").innerHTML = html;
        }
    }
    xhr.open("GET", "team.xml", true);
    xhr.send();
});
```

## How to Use the jQuery Shorthand Methods for Ajax

The Shorthand jQuery Methods for Working with Ajax:

  1. `load(url[, data][, success])` - Load HTML data
  2. `$.get(url[, data][, success][, dataType])` - Load data with a GET request.
  3. `$.post(url[, data][, success][, dataType])` - Load data with a POST request.
  4. `$.getJSON(url[, data][, success])` - Load JSON data with a GET request.

The Parameters for the Shorthand Methods:

  1. `url` - The string for the URL where the request is sent.
  2. `data` - A map or string that is sent to the server with the request, usually to filter the data that is returned.
  3. `success` - A callback function that is executed if the request is successful.
  4. `dataType` - A string that specifies the type of data (html, xml, json, script, or text). The default is XML.

The `$.each` method for processing the data that's returned: `$.each(collection, callback)` - The collection parameter is an object or array. The callback parameter is a function that's done for each item in the collection.

A load method - `$("#solution").load("solutions.html);`

A `$.get` method that includes data and calls a success function - `$.get("getmanager.php", "name=agnes", showManager);`

```javascript
//A `$.getJSON` method with an embedded success function
$.getJSON("team.json", function(data) {
    // the statements for the success function
})
```

```javascript
// jQuery that loads data when a link is clicked
$(document).ready(function() {
    $("#vprospect").click(function() {
        $("#soluction").load("solutions.html #vprospect");
    });
    $("#vconvert").click(function() {
        $("solution").load("#solutions.html #vconvert");
    });
    $("#vretain").click(function() {
        $("#solution").load("solutions.html #vretain");
    });
});
```

The load function can only load content from files on the same server as the page making the call.

To use the `$.get` and `$.post` methods the file(s) names in the URL have to be on a web server, not on a file server; specifically the XML file must be in the same domain as the web page that's making the request due to the *cross-domain security policy* used by most browsers.

```javascript
// jQuery using the $.get method to retrieve XML data
$(document).ready(function() {
    $.get("team.xml", function(data) {
        $("#team").html("");
        $(data).find("management").children().each(function() {
            var xmlDoc = $(this);
            $("#team").append("<h3>" +
                xmlDoc.find("name").text() + "<h3>" +
                xmlDoc.find("title").text() + "<br>" +
                xmlDoc.find("bio").text() + "<br>");
        });
    });
});
```

```javascript
// jQuery using the $.getJSON method to retrieve JSON data
$(document).ready(function() {
    $.getJSON("team.json", function(data) {
        $.each(data, function() {
            $.each(this, function(key, value) {
                $("#team").append(
                    "Name: " + value.name + "<br>" +
                    "Title: " + value.title + "<br>" +
                    "Bio: " + value.bio + "<br><br>"
                );
            });
        });
    });
});
```

The Helper Methods for Working with Ajax:

  1. `serialize()` - Encode a set of form elements as a string that can be used for the data parameter of an Ajax request.
  2. `serializeArray()` - Encode a set of form elements as an array of name/value pairs that can be used for the data parameter of an Ajax request.

```javascript
// jQuery that uses the serialize method
$(document).ready(function() {
    var formData = $.("#contactForm").serialize();
    $.get("processcontact.php", formData, processReturnedData);
    function processReturnedData(data) {
        // the statements for the success function
    }
});
```

## How to Use the $.ajax Method for Working with Ajax

Syntax of the `$.ajax` method - `$.ajax({ options })`

Some of the options for the `$.ajax` method:

  1. `url` - The string for the URL where the request is sent.
  2. `beforeSend(jqXHR, settings)` - A function that is executed before the request is sent. It can pass two parameters: the jqXHR object and a map for the settings for this object.
  3. `cache` - A Boolean value that determines if the broswer can cache the response.
  4. `complete(jqXHR, status)` - A function that is executed when the request finishes. It can receive two parameters: the jqXHR object and a string that represents the status of the request.
  5. `data` - A map or string that is sent to the server with the request, usually to filter the data that is returned.
  6. `dataType` - A string that specifies the type of data (html, xml, json, script or text).
  7. `error(jqXHR, status, error)` - A function that is executed if the request fails. It can receive three parameters: the jqXHR object, a string that represents the type of error, and an exception object that receives the text portion of the HTTP status.
  8. `jsonp` - A string containing the name of the JSONP parameter to be passed to the server. Defaults to "callback".
  9. `password` - A string that contains a password that will be used to respond to an HTTP authentication challenge.
  10. `success(data, status, jqXHR)` - A function that is executed if the request is successful. It can receive three parameters: the data that is returned, a string that describes the status, and the jqXHR object.
  11. `timeout` - The number of milliseconds after which the request will time out in failure.
  12. `type` - A string that specifies the GET or POST method.
  13. `username` - A string that contains a user name that will be used to respond to an HTTP authentication challenge.

*jqXHR* stands for "jQuery XHR object" and is a superset of the regular XHR object which contains all of the normal XHR properties as well as some others.

*JSONP* stands for "JSON with Padding" and is a method of bypassing the cross-domain security policies and allowing one to request data from a server in a different domain.

```javascript
// jQuery showing the use of the $.ajax method
$(document).ready(function() {
    $.ajax({
        type: "get",
        url: "team.xml",
        beforeSend: function() {$("#team").html("Loading...");},
        timeout: 10000,
        error: function(xhr, status, error) {
            alert("Error: " + xhr.status + " - " + error);
        },
        dataType: "xml",
        success: function(data) {
            $("#team").html("");
            $(data).find("management").children().each(function() {
                var xmlDoc = $(this);
                $("#team").append("<h3>" +
                    xmlDoc.find("name").text() + "</h3>" +
                    xmlDoc.find("title").text() + "<br>" +
                    xmlDoc.find("bio").text() + "<br>");
            });
        }
    });
});
```

## How to Use Ajax with Flickr

The URL for the Flicr public feed documentation - `www.flickr.com/services/feeds/docs/photos_public/`

Flickr feeds:

  1. **Public photos & video** - Returns public content matching specified criteria.
  2. **Friends photostream** - Returns public content from the contacts, friends, and family of a specified user.
  3. **Public favorites from a user** - Returns public favorites for a specified user.
  4. **Group discussions** - Returns recent discussions from a specified group.
  5. **Group pools** - Returns items recently added to the pool of a specified group.
  6. **Forum discussions** - Returns recent topics from the Flickr forums.
  7. **Recent activity** - Returns recent activity for a specified user.
  8. **Recent comments** - Returns recent comments by a specified user.

The base URL for retrieving a public photo stream - `http://api.flickr.com/services/feeds/photos_public.gne`

The common query parameters for the public photos feed:

  1. `id` - A user id.
  2. `ids` - A comma-delimited list of ids.
  3. `tags` - A comma-delimited list of tags that identify the photos.
  4. `tagmode` - Controls whether the returned items must match all of the tags specified or any of the tags specified. The default is all.
  5. `format` - The format of the returned feed. Atom 1.0 is the default.
  6. `lang` - The display language of the feed. The default is English.
  7. `jsoncallback` - Optional unless the return format is set to JSON. Then, this parameter must be coded as `jsoncallback=?`.

A URL that gets a JSON feed for a specific user id (in one line): `http://api.flickr.com/services/feeds/photos_public.gne?id=82407828@N07&format=json&jsoncallback=?&tags=vectacorp`

A URL that gets a JSON feed for all users (in one line): `http://api.flickr.com/services/feeds/photos_public.gne?&format=json&jsoncallback=?&tags=waterfall,yosemite`

Data items returned by a photo feed:

  1. `items` - The collection of returned items.
  2. `title` - The title of the photo.
  3. `link` - The URL for the Flickr page for the photo.
  4. `media.m` - The URL for the photo.
  5. `date_taken` - The date the photo was taken.
  6. `description` - Descriptive text for a photo, plus a thumbnail image in an `<a>` element that links to the full photo on the Flickr site. This data is formatted with HTML tags so it's ready for display.
  7. `published` - The date and time the photo was uploaded to Flickr.
  8. `author` - The author's username and email.
  9. `author_id` - The author's id.
  10. `tags` - The filtering tags for a photo.

```javascript
// jQuery code that gets the titles and photos from a Flickr photo feed.
var url = "http://api.flickr.com/services/feeds/photos_public.gne?" +
          "format=json&jsoncallback=?&tags=waterfall,yosemite";

$.getJSON(url, function(data) {
    var html = "";
    $.each(data.items, function(i, item) {
        html += "<h2>" + item.title + "</h2>";
        html += "<img src=" + item.media.m + ">";
        html += "<p></p>";        
    });

    $("#photos").html(html);
});
```

The query urls can be pasted into the browser bar in order to see the contents of he JSON object

```javascript
// jQuery used to utilize the Flickr API to search Flickr by tag
$(document).ready(function() {
    var searchTerm;
    $("#btnSearch").click(function() {
        searchTerm = "";
        if ($("#search").val() == "") {
            alert("You must enter one or more tags!");
        }
        else {
            searchTerm = $("#search").val();

            var url =
                "http://api.flickr.com/services/feeds/photos_public.gne?" +
                "format=json&jsoncallback=?&tags=" + searchTerm + "&tagmode=all";

            $.getJSON(url, function(data) {
                var html = "";
                $.each(data.items, function(i, item) {
                    html += "<h2>" + item.title + "</h2>";
                    html += "<img src=" + item.media.m + ">";
                    html += "<p><b>Tags: </b>" + item.tags + "</p>";
                });
                $("#photos").html(html);
            });
        }
    });
});
```

***

### END CHAPTER

Robert Juall

07DEC2016