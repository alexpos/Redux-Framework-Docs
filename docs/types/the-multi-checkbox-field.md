---
category: Documentation
status:
group: Field Types
title: "The Multi Checkbox Field"
tags: 
layout: page
---

The multi checkbox field is an enhancement of a basic field type. It's just a group of checkbox inputs that is saved as an array of values (1 for checked, 0 for not checked).

To creat a multi checkbox field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'multi_checkbox', //the field type
    'title' => __('Multi Checkbox Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
    'options' => array('1' => __('Checkbox 1, 'nhp-opts')', '2' => __('Checkbox 2', 'nhp-opts')),// You must provide a set of key => value pairs
    'std' => array('1' => '1', '2' => '0') //See how it's changed from the std checkbox?
    )
?>
{% endhighlight %}

With the above array we will be creating a multi checkbox field with the options:

**id** 1

**title** Multi Checkbox Option

**options** Explained further down


These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.


We have also set the ```std``` attribute to an array of ```key => value``` where a value of 1 checks the box, this isn't required but allows you to set a default value when the theme is activated, or when the user hits reset. If you don't want to set it, you can remove this from the array.

You will also notice there is a ```Options``` section in the array. This is where you define the ```ID``` and ```title``` of each checkbox. It needs to be provided as a ```key => value``` pair for each checkbox in the field type.