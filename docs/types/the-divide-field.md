---
category: Documentation
status: 
group: Non Value Field Types
title: "The Divide Field"
tags: 
layout: page
---

The divide field is just a non option field which divides the page output as to not over load a user with information.

It basically closes the form table, adds a hr line element, then reopened the options table.

This field requires only the type and Id attributes to be set, no the options are needed.

Example:

{% highlight php %}
<?php
array(
    'id' => '21',
    'type' => 'divide'
),
?>
{% endhighlight %}
