# ProcessWire Unique Text Fieldtype

This is the same as the ProcessWire Text field (FieldtypeText), but 
enforces that values stored are unique, site-wide.

### Requirements

Requires ProcessWire 3.0.150 or newer. 

### To install

Place the files for this module in `/site/modules/FieldtypeTextUnique/`, 
and then install from the Modules admin screen.

### To upgrade

This module is a rewrite of the previous version which was released in 2013.
The ProcessWire core now has some unique index tools included in it, which 
this module uses. If you are using the previous version, please backup your
database before upgrading, just to play it safe. Then replace the files in
`/site/modules/FieldtypeTextUnique/` with those from the new version. 

### To use on a new field

Create a new field (Setup > Fields > Add New) and choose “Text Unique” as 
the type. Configure the Details and Input tabs the same way that you would
with a regular Text field. 

### To use on an existing field

You may also convert an existing Text field to Text Unique. To do so, edit 
the field (Setup > Fields > your_text_field) and then change the type to 
“Text Unique”. Note that the existing field must not have any duplicate values. 
If the field does have duplicate values then the type change will produce an 
error message in the admin to that effect. Remove any duplicates and try again.

Note that this Fieldtype is not a multi-language Fieldtype, so you should not
attempt to convert multi-language text fields to Text Unique fields. 

### How it works

The Text Unique Fieldtype works the same as the Text Fieldtype and uses the 
same Text Inputfield. The only difference is that a UNIQUE index is applied 
on the `data` column that stores the text so that each value can only be 
entered once per page. 

If the user attempts to enter the same value on more than one page then it 
will be changed back to their previous value and an error message is reported
indicating that the value they entered is not unique, along with the page ID
that contains the colliding value. 

### Please note

The first 191 characters of the text value are what determines whether or 
not the value is unique. If two values are the same for the first 191 
characters but differ after that, they will still collide. This seemingly
arbitrary number is actually the max index length for MySQL when used with
the InnoDB engine and the UTF8MB4 charset, so the actual number will depend
somewhat on your DB configuration. 

---
Copyright 2021 by Ryan Cramer

