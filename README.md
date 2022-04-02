# flask-appbuilder-ovveride-form

Flask-appbuilder is a great module to manage CRUD operations on databases, but for a specific application I needed to completely redefine some views while maintaining access to the database, without using the module's standard grid interface.
The documentation indicates how to replace the templates for individual activities, but is completely lacking in how to interact with the forms used internally by the application.
To write a truly custom view this information is essential, but it seems there is no information about that over the internet. So I decided to exctract that directly from sources.

The main code calls the view render module passing a data structure called *widgets* that contains all the variables needed to render the view. However that data need to be reordanized to be used directly in a standard WTForms template. Moreover, the internal structure of widgets is depending upon the action choosed (add/edit/show).
So I've decided to write a simple jinja2 code fragment to exctract the fields needed, fillig two dictionary, one to hold label strings (label), the other one to hold related values (data).
In my application I use two different templates, one for add/edit and another one for show, but however is quite simple to merge the fragments if a single template is in use.

Just a notice: for edit/add code to work all fields present in widgets data structure must me handled by the form inside the template. So be carefull to exclude unused fields using add_exclude_columns and/or edit_excluded_columns in view definition code.
