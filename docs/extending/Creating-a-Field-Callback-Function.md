---
layout: page
title: Creating a field callback function
category: Documentation
group: Extending the Framework
tags:
---

Creating a field callback function is quite similar to creating a field class. The reason it's available is for very specific/custom fields.

So for example if you wanted a field class to be used more than once in the options panel, you would be better creating a field class (and letting us know about it so we can maybe include it in the core).

But if you wanted a field thats only going to be used once, you should use a callback.

**Note** If this custom callback needs CSS or JavaScript to be included you will need to use the built in actions to add to the page.

Okay so say for example we want a custom use function for 1 field in the form, which displays a custom input (for the example we are just going to use a checkbox input, but it can be anything you want).

When declaring the field in the ```php$sections``` field array instead of calling ```php'type' => 'field_type'```, we would call ```php'callback' => 'your_func_name'```.

Then you would need to call a function called ```phpyour_func_name```.

This function will be passed two parameters:

{% highlight php %}
function your_func_name($field, $value){

}//function
{% endhighlight %}

**$field** is an array of all the attributes declared when adding the field to the ```php$sections``` array.

**$value** is the current value in the database. This could be an array, a string, or null depending on the field type and if it has been saved yet.

So then it's simply a case of checking what the ```php$value``` is and doing something based on that (in this case checking the box). 

**Note** When defining the field array you can add as many or as little additional prams when using a custom callback, they will all be passed back to the function in the field array.

**Note** When creating input fields they must have a specific naming structure to be saved in the db when using the settings API. This naming structure is ```phpoption_name[id_of_option]```.

If you defined a custom option name you need to use that for the first part. If not the option name is the theme name in lowercase with white space replaced by underscores. For this example I am using the Twenty Eleven theme so the option name would look like this:


{% highlight php %}
twenty_eleven[option_name]
{% endhighlight %}


Also note that if this is a multi value field like multi checkboxes, or multi select fields you need to add another set of square brackets to the name like so:


{% highlight php %}
twenty_eleven[option_name][]
{% endhighlight %}


This should always be passed as the ```php name="" ``` part of the field input.


Okay so let's look at the function itself:

{% highlight php %}
Function your_func_name($field, $value){

echo '<label for="tewenty_eleven['.$field['id'].']">';
echo '<input type="checkbox" name="tewenty_eleven['.$field['id'].']" '.checked($value, '1', false).'/>';
echo $field['desc'];
echo '</label>';

}//function
{% endhighlight %}

Here we are simply echoing the checkbox field, and using the buit in WordPress function ```phpchecked()``` to see if the option is set to "checked".

And thats it, it can be as simple or as complex as you need it. You can also call as many custom callbacks functions as you like (1 per field) so the power is in your hands.