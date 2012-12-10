---
category: Documentation
status: 
group: Field Types
title: "The Multi Select Field"
tags: 
layout: page
---

The multi_select field is a basic field type. It's just a drop down select input where multiple options can be selected.

To creat a multi_select field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'multi_select', //the field type
    'title' => __('Multi Select Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
    'options' => array('1' => __('Option 1', 'nhp-opts'), '2' => __('Option 2', 'nhp-opts')),// You must provide a set of key => value pairs
    'std' => array('1', '2')//this should be the key as defined above
    )
?>
{% endhighlight %}

With the above array we will be creating a radio field with the options:

**id** 1

**title** Multi Select Option

**options** Explained further down


These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.


We have also set the ```std``` attribute to an array of  ```'1', '2'``` this will automatically select the options 1, and 2 from the select input.

You will also notice there is a ```Options``` section in the array. This is where you define the ```Option value``` and ```title``` of each select option. It needs to be provided as a ```key => value``` pair for each select option in the field type.