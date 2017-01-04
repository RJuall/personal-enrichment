# How to Script the DOM with Javascript

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 99

***

## DOM Scripting Properties and Methods

The *DOM Core Specification* defines the properties of the DOM and DOM scripting, implemented by all current browsers

The *Document Object Model (DOM)* is built as an HTML page is loaded into the browsers

The DOM contains *nodes* that represent all of the HTML elements and attributes for a page

As the DOM is changed, the web page changes to reflect the state of the DOM *(DOM Scripting)*

Types of DOM nodes include *element nodes*, *text nodes*, *attribute nodes*, and *comment nodes*

The properties and methods for working with DOM nodes are defined by a specification called an *interface*

Terms such as *parent*, *child*, *sibling*, and *descendant* are used to describe the relationships between nodes in a document

The *Node Interface* defines properties that can be used for working with nodes.

Some properties of the node interface include *nodeValue*, *parentNode*, *childNodes*, *firstChild*, *lastChild*, and *nextElementSibling*

Common methods of the document and element interfaces (all return arrays) - *getElementsByTagName(tagName)*, *getElementsByName(name)*, *getElementsByClassName(classNames)*

Common methods of the element interface (all return arrays) - *hasAttribute(name)*, *getAttribute(name)*, *setAttribute(name, value)*, *removeAttribute(name)*

How to create an array of all `<a>` tags in a document - `var links = document.getElementsByTagName("a");`

## The Email List Application

```javascript
var joinList = function () {
    var emailAddress1 = $("email_address1");
    //...
    var isValid = true;

    //validate the first entry
    if (emailAddress1.value == "") {
        emailAddress1.nextElementSibling.firstChild.nodeValue = 
            "This field is required.";
        isValid = false;
    } else {
        emailAddress1.nextElementSibling.firstChild.nodeValue = "";
    }
    //...
}
```

## The FAQs Application

The FAQs page is composed of *Collapsible Panels*

`<h2>` elements coded with embedded `<a>` elements so that the FAQ can be tabbed through and selected with the `Enter` key

```javascript
var $ = function (id) { return document.getElementById(id); };

// the event handler for the click event of each h2 element
var toggle = function () {
    var h2 = this;                      //refers to the clicked h2 tag
    var div = h2.nextElementSibling;    //div = h2's sibling div

    // toggle + and - image in h2 elements by adding or removing a class
    if (h2.hasAttribute("class")) {
        h2.removeAttribute("class");
    } else {
        h2.setAttribute("class", "open");
    }
};

window.onload = function () {
    // get the h2 tags
    var faqs = $("faqs");
    var h2Elements = faqs.getElementsByTagName("h2");

    // attach event handler for each h2 tag
    for (var i = 0; i < h2Elements.length; i++) {
        h2Elements[i].onclick = toggle;
    }
    // set focus on first h2 tag's <a> tag
    h2Elements[0].firstChild.focus();
};
```

## DOM Scripting Skills for Links and Images

```javascript
//DOM-compliant code that cancels the default action
var eventHandler = function(evt) {
    evt.preventDefault();
}
```

Above will not work with older IE implementations

```javascript
//How to create and preload an image Object
var image = new Image();
image.src = "image_name.jpg";

//How to preload all images referenced by the href attributes of <a> tags
var links = document.getElementsByTagName("a");
var i, link, image;
for (i = 0; i < links.length; i++) {
    link = links[i];
    image = new Image();
    image.src = link.href;
}
```

## The Image Swap Application

```javascript
$ = function(id) {
    return document.getElementById(id);
}

var swap = function(evt) {
    var link = this;
    var captionNode = $("caption");
    var imageNode = $("image");

    imageNode.src = link.getAttribute("href");
    captionNode.firstChild.nodeValue = link.getAttribute("title");

    //cancel the default action of the event
    if (!evt) { evt = window.event; }
    if (evt.preventDefault) {
        evt.preventDefault();   //DOM compliant code
    }
    else {
        evt.returnValue = false;
    }
}

window.onload = function() {
    var listNode = $("image_list");
    var imageLinks = listNode.getElementsByTagName("a");

    //process image links
    var i, linkNode, image;
    for (i = 0; i < imageLinks.length; i++ ) {
        //attach event handler
        linkNode = imageLinks[i];
        linkNode.onclick = swap;
        //preload image
        image = new Image();
        image.src = linkNode.getAttribute("href");
    }
    imageLinks[0].focus;
}
```

## How to Use Timers

*Timers* let one execute functions after a specified period of time, often used in DOM scripting

```javascript
setTimeout( *function*, *delayTime* );   //Creates a Timer
clearTimeout ( *timer* );                //Cancels a Timer
```

```javascript
//How to embed a timer function in the first parameter
//of the setTimeout method
window.onload = function() {
    var timer = setTimeout(
        function() {
            $("startup_message").setAttribute("class", "closed");
            clearTimeout(timer);
        },
    5000);
}
```

```javascript
//Working with a timer that calls a function repeatedly
setInterval ( *function*, *intervalTime* )
clearInterval ( *timer* )
```

## The Slide Show Application

```html
<main>
    <h1>Fishing Slide Show</h1>
    <h2 id="caption">Casting on the Upper Kings</h2>
    <img id="slide" src="images/casting1.jpg" alt="">
    <div id="slides">
        <img src="images/casting1.jpg" alt="Casting on the Upper Kings">
        <img src="images/casting2.jpg" alt="Casting on the Lower Kings">
        <img src="images/catchrelease.jpg"
             alt="Catch and Release on the Big Horn">
        <img src="images/fish.jpg" alt="Catching on the South Fork">
        <img src="images/lures.jpg" alt="The Lures for Catching">
    </div>
</main>
<!--
css - #slides img { display: none; }
-->
```

```javascript
var $ = function(id) {
    return document.getElementById(id);
}

window.onload = function() {
    var slidesNode = $("slides");
    var captionNode = $("caption");
    var imageNode = $("slide");

    var slides = slidesNode.getElementsByTagName("img");

    //start slide Show
    var image, imageCounter = 0;
    var timer = setInterval(
        function() {
            imageCounter = (imageCounter + 1) % slides.length;
            image = slides[imageCounter];
            imageNode.src = image.src;
            captionNode.firstChild.nodeValue = image.alt;
        },
    2000);
}
```

***

### END CHAPTER

Robert Juall

31OCT2016