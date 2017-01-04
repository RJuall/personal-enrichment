# How to Use the HTML5 APIs

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 437

***

## An Introduction to the HTML5 APIs

Some of the HTML5 APIs that are supported by all browsers:

  1. `Canvas` - Provides for creating graphs, game graphics, art, and other types of visual imagery.
  2. `classList` - Provides for retrieving and applying CSS classes to elements on a web page.
  3. `Constraint` - Provides for natively validating forms and form objects within the browser without the need for Javascript code.
  4. `Drag and Drop` - Provides for dragging elements on a web page and dropping them into a predefined target area within the same web page.
  5. `Geolocation` - Allows the browser to determine the latitude, longitude, altitude, heading, and more of the user browsing a geolocation-enabled site.
  6. `Page Visibility` - Provides for detecting whether a page is the active tab or window so the application can react accordingly.
  7. `Server-Sent Events` - Similar to the WebSocket API but limited to one-way communication from the server to the client.
  8. `Web Storage` - Replaces cookies as a simple method for persisting data between page requests.
  9. `Web Workers` - Provides for multi-threaded execution within a Javascript application. The main thread runs in the foreground while other threads run in the background.
  10. `Web Notifications` - Provides for an application displaying notifications to the user that appear outside of the broswer window. Icons, text, links, and more can be added to the notifications.
  11. `WebGL` - Provides for creating interactive 2D and 3D graphics within a web browser without the need for plugins.
  12. `WebSocket` - Provides for two-way communication between client-side and server-side applications. Useful for web-based chat applications, real-time, turn-based games, social media applications that inform users of updates to their feed and more.
  13. `Vibration` - Consists of a single method that sends a request to the user's device (smartphone, tablet, etc.) to initiate a vibration.

Sources of information about the HTML5 APIs:

  1. The Web Platform - `platform.html5.org`
  2. WHATWG - `whatwg.org`
  3. Mozilla Developer Network - `developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5`
  4. W3C - `www.w3.org/TR/html5` or `dev.w3.org/html5/spec`
  5. HTML5 Demos and Examples - `html5demos.com`
  6. w3schools - `www.w3schools.com/html`

## How to Use the Geolocation API

The HTML5 *Geolocation API* can be used to determine a User's location.

Properties of the coordinates object that defines a location:

  1. `latitude` - The latitude in decimal degrees.
  2. `longitude` - The longitude in decimal degrees.
  3. `accuracy` - The accuracy level in meters for the latitude and longitude coordinates.
  4. `altitude` - The height of the position in meters above the mean sea level.
  5. `altitudeAccuracy` - The accuracy level in meters for the altitude position.
  6. `heading` - The direction of travel in degrees from true north.
  7. `speed` - The current ground speed in meters per second.

```javascript
// jQuery code taht uses the Geolocation API
$(document).ready(function() {
    $("button").click(function (event) {
        navigator.geolocation.getCurrentPosition(function (position) {
            alert("Latitude: " + position.coords.latitude + "\n" +
            "Longitude: " + position.coords.longitude + "\n" +
            "Accuracy: " + position.coords.accuracy);
        });
    });
});
```

The latitude, longitude, and accuracy values are based on network signals such as IP addresses, cell phone IDs, cell tower triangulation, and GPS coordinates.

```javascript
// jQuery that shows the User's location on a Google Map
$(document).ready(function() {
    navigator.geolocation.getCurrentPosition(function(position) {
        var url =
            "http://maps.google.com/maps/api/staticmap?sensor=false" +
            "&center=" + position.coords.latitude + "," +
            position.coords.longitude +
            "&zoom=14&size=300x400&markers=color:red|" +
            position.coords.latitude + "," +
            position.coords.longitude;
        $("img").attr("src", url);
    });
});
```

When using the geolocation API it won't work if (1) the user won't share their location, (2) the geolocation service in the broser is unable to detect the User's position, or (3) the retrieval of the position times out.

These correlate to the errors `PERMISSION_DENIED`, `POSITION_UNAVAILABLE`, and `TIMEOUT`

```javascript
// Javascript that handles Geolocation errors
$(document).ready(function() {
    navigator.geolocation.getCurrentPosition(getLocation, errorHandling);

    function getLocation(position) {
        var url =
            "http://maps.google.com/maps/api/staticmap?sensor=false" +
            "&center=" + position.coords.latitude + "," +
            position.coords.longitude +
            "&zoom=14&size=300x400&markers=color:red|" +
            position.coords.latitude + "," +
            position.coords.longitude;
        $("img").attr("src", url);
    }

    function errorHandling(error) {
        switch(error.code) {
            case error.PERMISSION_DENIED:
                alert("Not sharing your location.");
                break;
            case error.POSITION_UNAVAILABLE:
                alert("Couldn't detect position.");
                break;
            case error.TIMEOUT:
                alert("Position retrieval timed out.");
                break;
            default:
                alert("Unknown error.");
                break;
        }
    }
});
```

## How to Use the Web Storage API

## An Application that Uses a Web Worker and Web Storage

***

### END CHAPTER

Robert Juall

__DEC2016