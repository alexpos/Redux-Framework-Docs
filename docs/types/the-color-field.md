---
category: Documentation
status:
group: Field Types
title: "The Color Field"
tags: 
layout: page
---

The color field is just a text field that has some jquery magic assigned to it. When the user clicks the field to input a color it pops up with a jquery color picker, which is called fantastic, and is what Wordpress uses for its custom background feature.

To creat a color field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'color', //the field type
    'title' => __('Color Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
    'std' => '#ffffff'
    )
?>
{% endhighlight %}

With the above array we will be creating a text field with the options:

**id** 1

**title** Color Option

These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.

By default the field will validate the input as a HTML color value and provide an error message if the user manually inputs an Invalid string.

You can also set the ```std``` attribute as we have above if required. This must be a valid color value prepended by a hash character.