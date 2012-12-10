---
category: Documentation
status:
group: Field Types
title: "The Date Field"
tags: 
layout: page
---

The date field is just a text field that has some jquery magic assigned to it. When the user clicks the field to input a date it popup with a jquery date picker, which by default uses the aristo theme, but can be overridden using the many class actions and filters.

To creat a date field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'date', //the field type
    'title' => __('Date Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts')
    )
?>
{% endhighlight %}

With the above array we will be creating a text field with the options:

**id** 1

**title** Date Option

These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.

By default the field will validate the input as a date and provide an error message if the user manually inputs an Invalid date string.
