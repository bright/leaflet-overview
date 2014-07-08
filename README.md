# L.Control.Overview
Provides an overview map that responds to base layer changes.

Fork of [areichman/leaflet-overview](https://github.com/areichman/leaflet-overview) 
that adds additional `onAfterInitLayout` hook that enables responding to overview map 
events etc. and removes the necessity to define layers for overview map separately -
this fork inherits the layers of the main map automatically.

## Setup
First, define two base layers and initialize the main map with the default base layer:

```javascript
var osm = L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
  name: 'osm',
  attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
});
          
var mqo = L.tileLayer('http://otile{s}.mqcdn.com/tiles/1.0.0/osm/{z}/{x}/{y}.png', {
  name: 'mapquest',
  attribution: 'Tiles courtesy of <a href="http://www.mapquest.com/">MapQuest</a>',
  subdomains: '1234'
});
          
var map = L.map('map', {
  layers: osm,
  center: [43.12, -77.67],
  zoom:   10
});
```

Next, add the layer switcher control to the map:

```javascript
L.control.layers({
  'OpenStreetMap': osm, 
  'MapQuest Open': mqo
}).addTo(map);
```

Last, define overview control - it will inherit the layers from the main map:

```javascript
L.control.overview({
  position: 'bottomleft',
  onAfterInitLayout: function (overview) {
    console.log(overview);
  }
}).addTo(map);
```

You can see the above code in action in the [example](http://notherdev.github.io/leaflet-overview/example/).

## License
L.Control.Overview is free software, and may be redistributed under the MIT-LICENSE.
