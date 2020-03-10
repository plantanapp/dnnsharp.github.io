# Datasource for multiple choice fields

The power and flexibility of a multiple choice field comes from:
* the items it can display
* and where those Items can be taken from (the source of the data - datasource)

The [multiple choice fields](/action-form/form-fields/form-fields-types/multiple-choice.html) that are available in [Action Form](https://www.dnnsharp.com/dnn/modules/action-form-builder) share a series of datasources like, but not limited to:
* Portal/Admin/Host pages
* Portals/Modules/Roles/Containers
* TimeZone list
* Year range
* [Items](items-datasource.html)
* [SQL Query](sql-query-datasource.html)
* [Server request (JSON)](server-request-json-datasource.html)

Even though they each have particularities, they do share one thing in common; the datasource should contain items with:
* **_Text_** (what is visible in the field and shown to the user)
* and **_Value_** (the value of the field in the background) which is optional; in case the Value is missing(not specified), it will take the value of _Text_ 

On the back-end, the _Text_ and _Value_ of a multiple choice field can be addressed by using the _[field_name:Text]_ and _[field_name:Value]_. (_[field_name]_ can also be used and usually references the value of the field but it is in a more human-readable format like csv instead of JSON array for the multiplechoice with checkboxes field)