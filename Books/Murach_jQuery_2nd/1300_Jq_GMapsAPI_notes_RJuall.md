# How to Use the API for Google Maps

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 411

***

## Introduction to Google Maps

The URL for the Google Maps API reference - `developers.google.com/maps/docummentation/javascript/reference`

Google Maps can be added to a website freely up to a certain number of map requests

An API 'key' will be needed in order to use the Maps API on a website so that Google can monitor useage of its service

The Google Maps API consists of *classes* that provide the methods and properties that you need for adding Google Maps to web pages.

The classes for adding a map to a web page:

  1. `Map(element, options)` (#Map) - This constructor creates a Map object. The first parameter specifies the DOM object for the HTML element that receives the map. The second parameter provides options for the map.
  2. `LatLng(latitude, longitude)` (#LatLng) - This constructor creates a LatLng object based on its latitude and longitude parameters.
  3. `MapTypeId` (#MapTypeId) - This class provides constants for the four map types: ROADMAP, HYBRID, SATELLITE, and TERRAIN.

The required options for the Map constructor:

  1. `zoom` - A number that provides the initial zoom level.
  2. `center` - A new LatLng object that identifies the center of the map.
  3. `mapTypeId` - A MapTypeId constant that specifies the map type.

```javascript
//How to use the three classes to create a map object
var mapOptions = {
    zoom: 8,
    center: new google.maps.LatLng(33.4936111, -117.1475),
    mapTypeId: google.maps.MapTypeId.ROADMAP
};
var map = new google.maps.Map($("#map").get(0), mapOptions);
```

The Google Maps API consists of *classes* that provide the methods and properties that are needed for adding Google Maps to web pages.

The Google Maps classes are referred to throught the google.maps *namespace*

A *constructor* for a *class* creates a new *object* from that class. For example, the constructor for the 'Map' class creates a Map object. Then, the methods of the class can be called from the Map object. The 'new' keyword must be used with any constructor.

The constructor for a Map object can include many options in its second parameter, but only the three in the table above are required.

To provide the value for the mapTypeId option, on of the *constants* in the MapTypeId class is used.

To provide the value for the center option, the 'new' keyword is used with the 'LatLng' constructor.

To create a 'Map' object, a jQuery selector is used to identify the HTML element that will receive the map. Then the get(0) method is used to get the DOM object for that element.

The script element for the Google Maps API - `<script src="https://maps.googleapis.com/maps/api/js?key=your_api_key&sensor=false"></script>`

The HTML for the `<div>` element that will receive the map - `<div id="map"></div>`

```javascript
//The jQuery to add a Google Map
$(document).ready(function() {
    var mapOptions = {
        zoom: 8,
        center: new google.maps.LatLng(33.4936111, -117.1475),
        mapTypeId: google.maps.MapTypeId.ROADMAP
    };
    var map = new google.maps.Map($("#map").get(0), mapOptions);
});
```

The API key for Google Maps is optional, though recommended

## How to Display Markers on a Map

The classes for geocoding and markers:

  1. `Geocoder()` - This constructor creates a Geocoder object that provides methods that communicate with Google servers and return geocodes.
  2. `Marker(options)` - This constructor creates a Marker object that marks a position on a map. Two of the commonly-used options are position, which gives the location of the marker as a LatLng object, and map, which identifies the map for the marker.

One of the methods of the Geocoder class:

  1. `geocode(request, callback)` - Sends a GeocoderRequest object to Google servers that contains an address or a location and returns a GeocoderResult object that contains the results in an array.

Two of the properties of the GeocoderRequest object:

  1. `address` - The address of the request as a string.
  2. `location` - The location of the request as a LatLng object.

Three of the properties of the GeocoderResult object:

  1. `address_components` - The components of the address. From this property, you can use long_name and short_name to get those properties.
  2. `formatted_address` - The formatted address as a string.
  3. `geometry.location` - The location of the request as a LatLng object. From this property, you can use the lat() and lng() methods to get the latitude and longitude of the location.

```javascript
//How to use the geocode method
var geocoder = new google.maps.Geocoder();
geocoder.geocode({address: "4340 N Knoll, Fresno, CA"}, function(results) {
    alert("Latitude for " + results[0].formatted_address + " is " +
          results[0].geometry.location.lat());
});
//How to create a marker object
var marker = new google.maps.Marker({
    position: new google.maps.LatLng(36.799793, -119.858135),
    map: map});     //Assuming the Map object is in a variable named 'map'
```

*Geocoding* refers to the conversio of addresses into locations, and vice versa. this conversion is done by the geocode method of the Geocoder class.

To add a marker to a map, create a Marker object.

### How to create an address list that displays markers

```html
<!-- The HTML for the map and links -->
<div id="map"></div>
<ul id="links">
    <li><a href="#">Los Angeles, CA</a></li>
    <li><a href="#">Temecula, CA</a></li>
    <!-- the li elements for other cities -->
</ul>
```

```javascript
//The jQuery
$(document).ready(function() {
    var geocoder = new google.maps.Geocoder();
    var myLatLng = new google.maps.LatLng(33.4936111, -117.1475);
    var mapOptions = {zoom: 8, center: myLatLng,
                      mapTypeId: google.maps.MapTypeId.ROADMAP};
    var map = new google.maps.Map($("#map").get(0), mapOptions);

    $("#links a").click(function() {
        var address = $(this).text();       // gets address from <a> element
        geocoder.geocode({address: address}, function(results) {
            new google.maps.Marker({
                position: results[0].geometry.location,
                map: map
            });
        });
    });
});
```

## How to Display Messages on a Map

The classes for adding messages to markers:

  1. `InfoWindow(options)` - This constructor creates an object that works as a message balloon for a marker. Its content option provides the content for the balloon, and the content can be coded with plain text or HTML.
  2. `OverlayView()` - This constructor creates an object that can be used to overlay objects on a map.
  3. `MapCanvasProjection` - An object is created from this class when the getProjection method of an OverlayView object is called.

One method of the InfoWindow class:

  1. `open(map, marker)` - Opens the message balloon for the map and marker.

Three methods of the OverlayView class:

  1. `draw()` - Draws or updates the overlay.
  2. `setMap(map)` - Adds the overlay to the map.
  3. `getProjection()` - Returns a MapCanvasProjection object for the overlay.

One method of the MapCanvasProjection class:

  1. `fromLatLngToContainerPixel(markerPosition)` - Returns the pixel coordinates for a marker's position.

Two methods of the Marker class:

  1. `getPosition()` - Gets the latitude and longitude coordinates of the marker.
  2. `setMap(map)` - Renders the marker on the specified map. If the parameter is 'null', it removes the marker from the map.

```javascript
//Adding messages to markers
$(docment).ready(function() {
    var marker;
    var geocoder = new google.maps.Geocoder();
    var myLatLng = new google.maps.latLng(33.4936111, -117.1475);
    var mapOptions = {zoom: 8, center: myLatLng,
        mapTypeId: google.maps.MapTypeId.ROADMAP};
    var map = new google.maps.Map($("#map").get(0), mapOptions);

    $("#links a").click(function() {
        var address = $(this).text();           // gets address from <a> element
        if (marker) { marker.setMap(null); }    // deletes current marker
        geocoder.geocode({address: address}, function(results) {
            marker = new google.maps.Marker({
                position: results[0].geometry.location,
                map: map
            });
            // adds message balloon
            var infoWindow = new google.maps.InfoWindow({
                content: "This is: <h3>" + address + "</h3>" 
            });
            infoWindow.open(map, marker);
        });
    });
});
```

## How to Display Driving Directions on a Web Page

The classes for retrieving and displaying driving directions:

  1. `DirectionsService()` - This constructor creates an object that can be used to retrieve driving directions from the Google server.
  2. `DirectionsRenderer()` - This constructor creates an object that can be used to render driving directions.
  3. `TravelMode` - This class provides constants for four travel modes: DRIVING, BICYCLING, TRANSIT, and WALKING.

One method of the DirectionsService class:

  1. `route(request, callback)` - Issues a directions request. Its first parameter is a DirectionsRequest object that has three required properties: origin (starting location), destination, and travel mode. This method returns a DirectionsResult object and a DirectionsStatus object.

Three methods of the DirectionsRenderer class:

  1. `setMap(map)` - Specifies the map for which directions will be rendered.
  2. `setPanel(panel)` - Specifies the HTML `<div>` element that will receive the directions.
  3. `setDirections(result)` - Renders the result of a directions request in a `<div>` element.

```javascript
// A typical directions request
var request = {
    origin: marker1.getPosition(),
    destination: marker2.getPosition(),
    travelMode: google.maps.travelMode.DRIVING
};
directionsService.route(request, function(result, status) {
    directionsRenderer.setDirections(result);
});
```

Three methods of the event namespace for using event handlers:

  1. `addListener(object, event, handler)` - Registers an event handler for an object and event. It returns an event object that has properties related to the event.
  2. `removeListener(listener)` - Removes the specified listener.
  3. `trigger(object, event)` - Fires the specified event for the specified object.

```javascript
// how to use the addListener method to register an event handler
google.maps.event.addListener(marker, "click", function(event) {
    // code for the event handler
});
```

### How to Display Driving Directions with a Map

```html
<!-- The HTML for the map and the directions panel -->
<div id="map"></div>
<div id="directions"></div>
```

```javascript
// The jQuery
$(document).ready(function() {
    var directionsService = new google.maps.DirectionsService();
    var markers = [];
    var myLatLng = new google.maps.LatLng(33.4936111, -117.1475);
    var mapOptions = {zoom: 8, center: myLatLng, mapTypeId: google.maps.MapTypeId.ROADMAP};
    var map = new google.maps.Map($("#map").get(0), mapOptions);

    var listener = google.maps.event.addListener(map, "click", function(event) {
        var marker = new google.maps.Marker({position: event.latLng, map: map});
        markers[markers.length] = marker;
        if (markers.length > 1) {
            google.maps.event.removeListener(listener);
            var directionsRenderer = new google.maps.DirectionsRenderer();
            directionsRenderer.setMap(map);
            directionsRenderer.setPanel($("#directions").get(0));
            var request = { origin: markers[0].getPosition(),
                destination: markers[1].getPosition(),
                travelMode: google.maps.TravelMode.DRIVING };
            directionsService.route(request, function(result, status) {
                if (status == google.maps.DirectionsStatus.OK) {
                    directionsRenderer.setDirections(result);
                }
            });
        }
    });
});
```

***

### END CHAPTER

Robert Juall

29NOV2016