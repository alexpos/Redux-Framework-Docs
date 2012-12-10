---
category: Documentation
status: 
group: Field Types
title: "The Checkbox Field"
tags: 
layout: page
---

The checkbox field is a basic field type. It's just a checkbox input that is saved as 1 if checked, and it does have many options.

To creat a checkbox field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'checkbox', //the field type
    'title' => __('Checkbox Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
    'std' => '1', //This is a default value, used to set the options on theme activation, and if the user hits the Reset to defaults Button, default is 0, or not checked.
    )
?>
{% endhighlight %}

With the above array we will be creating a checkbox field with the options:

**id** 1

**title** Checkbox Option


These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.


We have also set the ```std``` attribute to 1 (which checks the box), this isn't required but allows you to set a default value when the theme is activated, or when the user hits reset. If you don't want to set it, you can remove this from the array.