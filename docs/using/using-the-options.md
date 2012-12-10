---
layout: page
title: Using the options
category: Documentation
group: Using the Framework
tags:
---

To use the options created by the Framework you can either use the built in WordPress functions for options like so:

{% highlight php %}
<?php
$options = get_option('option_name');
?>
{% endhighlight %}

Where option_name will be the custom opt_name you set in the $args array when creating the panel, or the theme_name in lower case with spaces replaced by underscores.

This will return an array of the options available, so to use them, you simply do something with the array values.

{% highlight php %}
<?php
echo $options['unique_id'];
?>
{% endhighlight %}

where unique_id is the id set for the field when creating the section fields.


## Or you can use the Frameworks solution

The Framework comes with some functions which can be used to get the options, with you needing to remember the option name.

Just make sure when calling the class you assign it to a global var like so:

{% highlight php %}
<?php
global $NHP_Options;
$NHP_Options = new NHP_Options($sections, $args);
?>
{% endhighlight %}

Then you can use the two built in functions for options display **get();** and **show();**.

Using get, will "get" the option value from the main options array, so if you have a field with the id of "10", to get that option just call:

{% highlight php %}
<?php
global $NHP_Options;
$option_val = $NHP_Options->get('10');
?>
{% endhighlight %}

To echo the option you can call the **show** function:

{% highlight php %}
<?php
global $NHP_Options;
$NHP_Options->show('10');
?>
{% endhighlight %}

**Note** Using the show function on an array value (like multi select/checkbox values) will result in nothing being echoed.


Also if you would like to get the whole options array, just call the classes options var like so:

{% highlight php %}
global $NHP_Options;
$options_array = $NHP_Options->options;
{% endhighlight %}

**Note** you only need to declare the global command once per script, ideally at the top of the file, then you would just call the functions wherever you need them.