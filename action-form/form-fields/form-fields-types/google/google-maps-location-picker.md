# Google Maps - Location picker (Map Marker)

Added in Action Form 5.0.526, the field will allow you to:
* create/collect/store 
* display
  
location markers on a Google Map based on coordinates (latitude and longitude).
![Google Maps Location Picker](https://static.dnnsharp.com/documentation/google_maps_location_picker.png)

The field allows you to set:
* map center method (based either on user Geolocation or provided latitude/longitude location)
* map zoom level
![Location picker map settings](https://static.dnnsharp.com/documentation/google_maps_location_picker_settings.png)

On submit, the field generates a list of tokens which include data as following:
* all field data as JSON: _[\<fieldname\>]_
* map marker position as latitude and longitude: _[\<fieldname\>:lat]_, _[\<fieldname\>:long]_

The field can also be used to display marker or multiple markers on a map based on values provided in the markers area of field's settings as seen below.

Field settings           |  Field on website
:-------------------------:|:-------------------------:
![Google Maps Multiple Location Markers](https://static.dnnsharp.com/documentation/google_maps_display_multiple_markers.png)  |  ![](https://static.dnnsharp.com/documentation/google_maps_multiple_markers.png)

> Starting with [Action Form 5.0.656+](https://www.dnnsharp.com/download?p=AFORM&v=05.00.656) the Parameter fields also support tokens
> 
## Display marker with radius

You can also diplay a circle(radius) on the Action Form Google Map field by adding Parameters in the Circles section as seen in the screenshot below.

> The circles feature is available in [Action Form 5.0.656+](https://www.dnnsharp.com/download?p=AFORM&v=05.00.656)
> 
Field settings           |  Field on website
:-------------------------:|:-------------------------:
![Google Maps Circle, marker with radius settings](https://static.dnnsharp.com/documentation/google_map_circle_marker_with_radius.png)  |  ![Google Maps Circle, marker with radius](https://static.dnnsharp.com/documentation/google_map_circle.png)