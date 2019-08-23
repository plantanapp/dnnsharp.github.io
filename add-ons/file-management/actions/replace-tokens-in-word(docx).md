# Replace tokens in word document (DOCX)

> Feature was added in [File Management version 5.0.xx]()

Using this action you can generate documents, based on a template, by using tokens. In order to use it, your template document must use *plain text content controls* inserted in the document.

To insert the content controls, you must go to **_File>Options>Customize Ribbon_**, check the **_Developer_** checkbox under the Main Tabs dropdown and click OK(save).
![Enable Developers Tab](https://static.dnnsharp.com/documentation/filemanager/enable_developers_tab_in_Word_menu.png "Enable Developers Tab")

After this has been done, you can go inside the document and insert a content control by clicking **_Developer_** tab in menu > **_Plain Text Content Control_** under the *Controls* section.
![Insert Content Control](https://static.dnnsharp.com/documentation/filemanager/add_content_control_in_word_document.png "Insert Content Control")

Inside the content control you can write a placeholder(helptext) so you can see what should go there after tokenization (i.e.: User Name) and in the properties of the content control (with the newly added control selected, click *Properties* under the *Controls* section), inside the title, simply put the token that needs to be replaced after the document tokenization (i.e: [User:Username]).
![Edit Content Control](https://static.dnnsharp.com/documentation/filemanager/edit_content_control_properties.png "Edit Content Control")

The content of the control will be replaced with the value of the token if it exists or with token itself if it doesn't exist; you will still be able to see what token generated that content by hovering over the control or going into its properties.

You can set-up this action using the following parameters:

* **Description**: Something so you'd quickly know what this action is about;
* **Error Message**: The admins will also see the detailed error message. Leave empty to use the default message;
* **Condition**: This boolean expression is used to determine if this action will execute. Use it to enable or disable actions programatically. For example, you'd enable a ShowError action only if you've found an error let's say when you parsed a response from a web service. A common example is [HasRole:Administrators\|true] (which requires My Token to work) or [SomeField] == "Some Value". This field supports My Tokens. See More examples;
* **File Identifier**: This parameter can either be a file id or a portal relative path, meaning if the path to file inside the site is Portals/0/SomeFolder/SomeDoc.docx the path you should provide as a parameter should be SomeFolder/SomeDoc.docx. This field supports My Tokens;
* **Folder**: Where to save the newly generated file. This field supports My Tokens;
* **Pattern**: You can provide a pattern to use in order to name the files. If you leave it empty, a GUID will be generated. This field supports My Tokens;
* **Handle Duplicates**: If there is a file with the same name, you can either overwrite the existing file or rename the one being added. By default the new file will be renamed;
* **Output Token Name**: A name for the token in which to save the generated file id;
