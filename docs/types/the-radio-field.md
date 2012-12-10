---
category: Documentation
status: 
group: Field Types
title: "The Radio Field"
tags: 
layout: page
---

The Radio Field
The radio field is a basic field type. It's just a group of radio input where only one option can be selected.

To creat a radio field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'radio', //the field type
    'title' => __('Radio Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
    'options' => array('1' => __('Radio 1', 'nhp-opts'), '2' => __('Radio 2', 'nhp-opts')),// You must provide a set of key => value pairs
    'std' => '2'//this should be the key as defined above
    )
?>
{% endhighlight %}

With the above array we will be creating a radio field with the options:

**id** 1

**title** Radio Option

**options** Explained further down


These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.


We have also set the ```std``` attribute to ```2``` this will automatically set the option to value ```2``` and display that radio option as checked by default.

You will also notice there is a ```Options``` section in the array. This is where you define the ```Option value``` and ```title``` of each radio option. It needs to be provided as a ```key => value``` pair for each radio input in the field type.