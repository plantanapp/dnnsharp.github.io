# Google Places autocomplete

This field will allow you to add to your online forms an autocomplete field 
![Google Places autocomplete](http://static.dnnsharp.com/documentation/google_places_field.png "Google Places autocomplete")
that searches through **Google Places** and on the back-end creates tokens with detailed data about the selected place like *[fieldname]*(containing all data [formatted as JSON](https://developers.google.com/places/web-service/details#PlaceDetailsResults)), *[fieldname:lat], [fieldname:lng], [fieldname:viewport]* and *[fieldname:formatted_address]*.

The **Google places autocomplete** can return the following type of information about a place:
* basic data (no extra cost, except for the _FindPlace_ charge)
* contact
* atmosphere

> **Google Places** field was introduced in [Action Form 5.0.566](https://www.dnnsharp.com/download?p=AFORM&v=05.00.566)
> _The [costs](https://developers.google.com/maps/billing/understanding-cost-of-use#basic-data) resulted from using the Google Places APIs are entirely supported by the website owner/administrator and are linked/related to the API key that was used when setting up the field._