---
category: Documentation
status: 
group: Non Value Field Types
title: "The Info Field"
tags: 
layout: page
---

The info field allows you to create a row in the options, that has no values, just some additional info.

This is great for providing extended descriptions of complex options.

You only need to provide the ```id```,```Type```, and ```desc``` fields in the array for this field, like so:


{% highlight php %}
<?php
array(
    'id' => '23',
    'type' => 'info',
    'desc' => __('<p class="description">This is the info field, if you want to break sections up.</p>', 'nhp-opts')
),
?>
{% endhighlight %}
