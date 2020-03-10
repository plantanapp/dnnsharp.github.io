# SQL Query Datasource

When Using SQL Select as Datasource for a multiple choice field, the columns selected will be automatically assigned as follows:
* first column represents the Text (what is shown to the user)
* second column represents the Value (the back-end value of the field)

unless otherwise specified in the SQL Query (more details below).

A valid datasource for the **SQL Query datasource** type will look like:

| SELECT Username FROM Table | SELECT Username,Id FROM Table |
|:-------------:|:-------------:|
| when you want to show _the username_ to the user and the value behind it to be _the username_ as well     | when you want to show _the username_ to the user and the _id_ to be the value behind _the username_|

_SELECT Username,Id FROM Table_ will generally result in _Username_ being the Text and _Id_ being the value. This can be overridden by specifying which one is the Text and whcih one is the Value as follows: _SELECT Username as Value,Id as Text FROM Table_.

> for situations in which one of the columns included in the SQL Query is named Value or Text it will be considered literally the _Value_ or the _Text_ for the multiple choice field.