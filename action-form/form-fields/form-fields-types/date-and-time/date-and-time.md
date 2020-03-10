# Date And Time

This component consists of 2 subcomponent UI widgets: one for the date and one for the time selection process.

Allows users to select date and/or time. On submit, this field will generate the following tokens: _[FieldName](which yields the value), [FieldName:Date], [FieldNameDay], [FieldName:Month], [FieldName:Year], [FieldName:DayOfMonth], [FieldName:DayOfYear], [FieldName&:Time], [FieldName:Hour], [FieldName:Minute], [FieldName:Iso]_

### Display mode
The filed has multipe display options which can be selected from the Admin as follows:
![DatePicker display modes](http://s3.amazonaws.com/static.dnnsharp.com/documentation/datepicker_display_modes.png "datepicker display modes")

* __Clickable Textbox__ _(default mode)_ - which shows on the form just a textbox; when clicked, the textbox will open the datepicker in popup in order for the date/time to be selected from the date picker control.
  
* __Inline__ - this option will display the entire date picker control inline on your form. 
    > *__Inline__ was added in Action Form 5.0.420*
    ![Datepicker display inline setting](https://static.dnnsharp.com/documentation/datepicker_display_inline_setting.png)
* __Textbox with button__ - this option is considered a more manual mode of the datepicker and when using it we recommend to always add a validator; it is a textbox in which the user can type date/time but which also has an attached button that when clicked will open the date picker control in a popup. 
  > *__Textbox with button__ was added in Action Form 5.0.580*
  ![Datepicker display inline setting](http://s3.amazonaws.com/static.dnnsharp.com/documentation/datepicker_display_textbox_button_setting.png)




### Options

* DateTime Picker Type 
  * Date and Time
  * Date
  * Time
* DateTime Format

  * Optionally, provide a custom date/time format, the default format is _MM/dd/yyyy HH:mm_. Leave empty to take the server locale default format.

* Other Options for Datepicker \(JSON\)

  * Optionally provide a JSON object with other options to pass into the Date Picker options. For example, write _{ showWeeks: true }_, please check the [documentation](https://github.com/Gillardo/bootstrap-ui-datetime-picker).

  ![](https://s3.amazonaws.com/static.dnnsharp.com/documentation/2017/07/chrome_2017-07-07_12-29-10.png)

Note that when the Date and Time field is initialized with a value(a date), the custom date needs to respect the specified format(MM/dd/yyyy HH:mm) or you must set the format of the field to your date's format.

