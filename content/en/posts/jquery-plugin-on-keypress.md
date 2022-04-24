---
title: Writing a jQuery plugin to filter a table on keypress
date: 2008-10-19T12:00:06+09:00
description: Sample article showcasing basic Markdown syntax and formatting for HTML elements.
draft: false
hideToc: false
enableToc: true
enableTocContent: true
tags:
- javascript
- jquery
---

I recently had a requirement to filter a table as the user was typing.

I was able to write a jQuery plugin to do this in just six lines of code.

I want to use jQuery to add a keyup handler to my search box, and target table(s) via a selector parameter.

First, in order to extend functionality onto a selector, we add a new function to `$.fn`

```javascript
  $.fn.tableFilter = function(tableSelector) {
```

Then we want to get a reference to the table we're going to filter:

```javascript
    table = $(tableSelector);
```


and we'll write a function that will actually perform the filtering:

    updateTable = function() {

 

now, on every keypress we need a blank slate.  lets hide all the rows besides the header:

```javascript
    table.find('tr:gt(0)').hide();
````

then, we'll display the rows that match the text we've typed:


````javascript
        table.find('td:contains("' + $(this).val() + '")').parents('tr').show();
    }
````

and we'll assign the keypress of event of our textbox to our new filterfing function:

````
    $(this).keyup(updateTable);
  }
````

and bam! we're done:

```
$.fn.tableFilter = function(tableSelector) {

    table = $(tableSelector);   

    updateTable = function() {
        table.find('tr:gt(0)').hide();       
        table.find('td:contains("' + $(this).val() + '")').parents('tr').show();
    }

    $(this).keyup(updateTable);
}
```

The we just wire up our plugin like this

`$("#filter").tableFilter("#ProductGrid");`

View the plugin in action [http://s116742794.onlinehome.us/jquery/tablefilter.htm](here.)

Note that this is case sensitive. You can see how to add a case insensitive selector [here](http://www.ericmmartin.com/creating-a-custom-jquery-selector/.)


