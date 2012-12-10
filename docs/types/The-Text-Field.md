---
layout: page
title: The Text Field
category: Documentation
group: Field Types
tags:
---

The text field is the most basic field type available. It's just a text input, but it does have many options.

To creat a text field option you need to create an array within the $sections => fields array. Like so:

{% highlight php %}
<?php
array(
    'id' => '1', //must be unique
    'type' => 'text', //the field type
    'title' => __('Text Option', 'nhp-opts'),
    'sub_desc' => __('This is a little space under the Field Title in the Options table', 'nhp-opts'),
    'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
    'validate' => 'url',//if you want to validate the value
    'msg' => 'custom error message', //override the default validation error message for no_html
    'std' => '', //This is a default value, used to set the options on theme activation, and if the user hits the Reset to defaults Button
    'class' => '' //Set custom classes for the element, default is "regular-text"
    )
?>
{% endhighlight %}

With the above array we will be creating a text field with the options:

**id** 1

**title** Text Option

These are the only required fields, the rest can be removed if not wanted. But it's always a good idea to explain the option using the ```sub_desc``` and ```desc``` fields.

In the example I have set the ```validation``` attribute to ```url```. This will automatically validate the submitted value as a URL and if it isn't valid trigger the error handling and set the field value back to it's current state. If you don't want it validated just remove it from the array.

Below that we have also set a custom error message by supplying the ```msg``` attribute. If this isn't set the validation class will provide a generic error message for Urls. This is only available if the field uses a validation method that triggers errors. Validation like stripping HTML or escaping JavaScript don't provide errors.

We have also left the ```std``` attribute as blank, this isn't required but allows you to set a default value when the theme is activated, or when the user hits reset. If you don't want to set it, you can remove this from the array.

We have also left the ```class``` attribute as empty. This will make the field use the standard class of **regular-text**. Again if you want it to be standard just ommit it from the array.
