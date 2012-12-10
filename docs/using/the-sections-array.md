---
layout: page
title: The $sections array
category: Documentation
group: Using the Framework
tags:
---

The $sections array is the core array for setting up the Framework class.

This array IS required and is the first parameter when calling the Framework class.

{% highlight php %}
<?php
new NHP_Options($sections, $args);
?>
{% endhighlight %}

A working example of the attributes is included in the **theme-options.php** file for you to see, but we're are going to look through the settings below.

To create multiple tabs, you just need to specify multiple $sections arrays.

Each attribute is an element in the array $sections.

{% highlight php %}
<?php
$sections[] = array(
        'icon' => trailingslashit(get_template_directory_uri()).'options/img/glyphicons/glyphicons_107_text_resize.png',
        'title' => __('Text Fields', 'nhp-opts'),
        'desc' => __('<p class="description">This is the Description. Again HTML is allowed</p>', 'nhp-opts'),
        'fields' => array(
                      array(
                            'id' => '1',
                            'type' => 'text',
                            'title' => __('Text Option', 'nhp-opts'),
                            'sub_desc' => __('This is a little space under the Field Title in the Options table, additonal info is good in here.', 'nhp-opts'),
                            'desc' => __('This is the description field, again good for additional info.', 'nhp-opts'),
                            'validate' => '', 
                            'msg' => 'custom error message',
                            'std' => '',
                            'class' => ''
                         )
                       )
              );
?>
{% endhighlight %}


***


{% highlight php %}
'icon' => trailingslashit(get_template_directory_uri()).'options/img/glyphicons/glyphicons_107_text_resize.png'
{% endhighlight %}

You can specify a custom icon for the section, square black icons are best. You can use the glyphicons included in the options framework if you like, there's plenty. You also could NOT set this, there is a default icons picked if you dont pass it in the array.


***


{% highlight php %}
'title' => __('Text Fields', 'nhp-opts')
{% endhighlight %}

As it suggests this is the title of the section, this is required. Sorry no HTML here.


***


{% highlight php %}
'desc' => __('<p class="description">This is the Description. Again HTML is allowed</p>', 'nhp-opts')
{% endhighlight %}

The description field can be used to pass "intro" content to the top of the section tab. This is optional, and HTML is allowed.


***


{% highlight php %}
'fields' => array()
{% endhighlight %}

The fields array is where you define your options. This attribute has multiple values, and each field type has different attributes, so there is a seperate page for each field type. Visit the [WIKI](https://github.com/leemason/NHP-Theme-Options-Framework/wiki "WIKI") homepage to see a list of the current Field types.
