Leaflet.GeoJSON.Ajax
====================
Leaflet extension for remote geoJson layers (Markers, Polylines, Polygons, ...) using AJAX.

Get collection of features from a remote `<URL>` & display it into the map with related & parametrables markers, lines & polygons.

Add customized markers, popup labels & click to navigate to external urls.

It depends on [Leaflet.Rrose](https://github.com/erictheise/rrose).

This plugin works both on Leaflet V0.7 & V1.0

DEMO
----
[See a DEMO using Leaflet V0.7](http://dominique92.github.io/MyLeaflet/github.com/Dominique92/Leaflet.GeoJSON.Ajax/)

[See a DEMO using Leaflet V1.0](http://dominique92.github.io/MyLeaflet/github.com/Dominique92/Leaflet.GeoJSON.Ajax/test/index-v1.0.html)

Usage
-----
### For a geoJson remote URL:
Create a L.GeoJSON.Ajax instance & add it to the map.
```javascript
...
Include stylesheets/leaflet.rrose.css and javascripts/rrose-src.js

new L.GeoJSON.Ajax(
	<URL>, // GeoJson server URL.
	{
		proxy: '', // Optional: insert proxy @ before the url
		bbox: false|true, // Optional: whether or not add bbox arg to the geoJson server URL
		argsGeoJSON: {
			name: value, // GeoJson args pairs that will be added to the url with the syntax: ?name=value&...
			...
		}
		style: function(feature) { // Optional
			return {
				"<NAME>": <VALUE>, // Properties pairs that will overwrite the geoJson flow features properties
				"<NAME>": feature.properties.<NAME>, // The value can be calculated from any geoJson property for each features.
				...
			};
		}
	}
).addTo(map);
...
```

### Properties pairs `"<NAME>":<VALUE>` can be:
* `title: <string>,` // hover label
* `popupAnchor: [<int>, <int>] | default=[middle,top+5px]`, // point from which the popup should open relative to the iconAnchor
* `url: <string>,` // url where to navigate when the feature is clicked

Or any of the following [L.GeoJSON options](http://leafletjs.com/reference.html#geojson-options)

Markers:
* `iconUrl: <string>,` // url of icon image
* `iconSize: [<int>, <int>] | default=img file size,` // Size of the icon.
* `iconAnchor: [<int>, <int>] | default=[middle,top],` // point of the icon which will correspond to marker's location
* `degroup: <int>,` // Isolate too close markers by a number of pixels when the mouse hover over the group.

Or any of the following [L.Marker options](http://leafletjs.com/reference.html#marker-options)

Poly*
Any of the following [L.Path options](http://leafletjs.com/reference.html#path-options)

### <geoJson> URL return must respect the [geoJson format](http://geojson.org/geojson-spec.html):
```javascript
{
	"type": "Feature",
	"geometry":
	{
		<geoJson geometry>...
	},
	"properties":
	{
		"<NAME>": <VALUE>, // Properties pairs that can be overloaded by the GeoJSON options or style
		...
	}
}
```

### Display local geoJson data with local style:
```javascript
Include stylesheets/leaflet.rrose.css and javascripts/rrose-src.js

new L.GeoJSON.Style(
	<geoJSON>, // <String> geoJson features
	{
		<OPTIONS>,
		"<NAME>": <VALUE>, // Optional: Properties pairs that will overwrite the geoJson flow features properties
		style: function(feature) { // Optional
			return {
				"<NAME>": <VALUE>, // Properties pairs that will overwrite the geoJson flow features properties
				"<NAME>": feature.properties.<NAME>, // The value can be calculated from any geoJson property for each features.
				...
			};
		}
	}
).addTo(map);
```

### Code example:
[GeoJSON.Ajax.WRI.js](https://github.com/Dominique92/Leaflet.GeoJSON.Ajax/blob/master/src/GeoJSON.Ajax.WRI.js)
