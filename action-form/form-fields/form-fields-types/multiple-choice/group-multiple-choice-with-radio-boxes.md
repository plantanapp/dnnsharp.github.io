# Group Multiple choice (with radio boxes)

> Available starting with [Action Form 5.0.615](http://www.dnnsharp.com/download?p=AFORM&v=05.00.615)

Similar to how a Button Group field type groups buttons, this field will group [Multiple choice (with radio boxes)](/action-form/form-fields/form-fields-types/multiple-choice/multiple-choice-with-radio-boxes.html) fields in order to make them act like a **Radio Buttons Grid** as seen in the image below.
![Radio Buttons Grid](https://static.dnnsharp.com/documentation/radio_buttons_grid_layout.png)

The Group Multiple Choice field will render only the selected [Multiple choice (with radio boxes)](/action-form/form-fields/form-fields-types/multiple-choice/multiple-choice-with-radio-boxes.html) fields as a grid by displaying each of them on a row and using the Item text(from datasource) as column title.

**Limitations**:
* all fields need to have the same number of items (prefferably the same datasource)
* each element of the group(row) will be evenly split on the row by following the formula: _container row width / (columns taken by title + number of items)_. For a label that takes 1 column and 3 radio buttons each of the elements(laber or radio button) will take up 25% of the row (_100/(1+3)_)

The functionality of each individual **_Multiple choice (with radio boxes)_** field will not be affected in any way; the selection for each field will still be stored in the token corresponding to the field itself and not to the Group field. The Group field just makes visual modifications.

The order of the fields in the group is determined by the order they appear in the admin of the Group field and not by the one specified in Action Form Layout
![Order of fields in radio Buttons Grid](https://static.dnnsharp.com/documentation/order_of_fields_in_radio_buttons_grid.png)

The number of columns taken by the label will decrease the remaining space available for the selectable items(radio buttons).