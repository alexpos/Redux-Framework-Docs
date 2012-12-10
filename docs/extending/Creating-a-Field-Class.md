---
layout: page
title: Creating a field class
category: Documentation
group: Extending the Framework
tags:
---

Creating a Custom Field Class for the Theme Options Framework, it quite simple. There are multiple Fields already, so taking a look at these can help to understand the proccess. These are located in the **options/fields** folder like so: **/options/fields/\*/field_\*.php**

Lets take a look at a custom field, for this example we are going to look at the most basic example field, a text field.

This is what the code looks like in the **/options/fields/text/field_text.php** file

{% highlight php %}
<?php

class NHP_Options_text extends NHP_Options{ 
    
    /**
     * Field Constructor.
     *
     * Required - must call the parent constructor, then assign field and value to vars, and obviously call the render field function
     *
     * @since NHP_Options 1.0
    */
    function __construct($field = array(), $value = ''){
        
        parent::__construct();
        $this->field = $field;
        $this->value = $value;
        
    }//function
    
    
    
    /**
     * Field Render Function.
     *
     * Takes the vars and outputs the HTML for the field in the settings
     *
     * @since NHP_Options 1.0
    */
    function render(){
        
        $class = (isset($this->field['class']))?$this->field['class']:'regular-text';
        
        echo '<input type="text" id="'.$this->field['id'].'" name="'.$this->args['opt_name'].'['.$this->field['id'].']" value="'.$this->value.'" class="'.$class.'" />';
        
        echo ($this->field['desc'] != '')?' <span class="description">'.$this->field['desc'].'</span>':'';
        
    }//function


    /**
     * Enqueue Function. (optional)
     *
     * If this field requires any scripts, or css define this function and register/enqueue the scripts/css
     *
     * @since NHP_Options 1.0
    */
    function enqueue(){
        
        wp_enqueue_script(
            'nhp-opts-field-text-js',//unique name
            $this->args['theme_url'].'options/fields/text/field_text.js', //can be any url
            array('jquery', 'farbtastic'),//requires
            time(),//expires
            true//in footer
        );
        
    }//function
    
}//class
?>
{% endhighlight %}


Okay, lets break it down a little.


***


### Class Definition ###

Firstly we need to take note of defining the class and name:

{% highlight php %}
class NHP_Options_text extends NHP_Options
{% endhighlight %}

The NHP Theme Options Framework uses a naming structure for field classes, so you **MUST** make sure you name custom classes like so:

{% highlight php %}
class NHP_Options_myclassname extends NHP_Options
{% endhighlight %}

When calling the custom field class for a field in the theme options you would define the type as **myclassname**

So a custom class called "example" would be declared like so:

{% highlight php %}
class NHP_Options_example extends NHP_Options
{% endhighlight %}


***


### Class Constructor ###

Now lets take a look at the classes constructor (required)

{% highlight php %}
/**
 * Field Constructor.
 *
 * Required - must call the parent constructor, then assign field and value to vars, and obviously call the render field function
 *
 * @since NHP_Options 1.0
 */
function __construct($field = array(), $value = ''){
        
    parent::__construct();
    $this->field = $field;
    $this->value = $value;
        
}//function
{% endhighlight %}

Here we need to call the parent class constructor so we can use the defined options

{% highlight php %}
parent::__construct();
{% endhighlight %}

Then we assign the passed vars **$field** (array from theme-options.php file), **value** (the current value in the database for this field)

{% highlight php %}
$this->field = $field;
$this->value = $value;
{% endhighlight %}


***


### Class Render Function ###

Then we need to create the **render();** function, this will need to echo its content and this is what is displayed in the options form for that field.

{% highlight php %}
/**
 * Field Render Function.
 *
 * Takes the vars and outputs the HTML for the field in the settings
 *
 * @since NHP_Options 1.0
 */
function render(){

 $class = (isset($this->field['class']))?$this->field['class']:'regular-text';

 echo '<input type="text" id="'.$this->field['id'].'" name="'.$this->args['opt_name'].'['.$this->field['id'].']" value="'.$this->value.'" class="'.$class.'" />';

 echo ($this->field['desc'] != '')?' <span class="description">'.$this->field['desc'].'</span>':'';

}//function
{% endhighlight %}

The render function first needs to assign a class to the field type (if you want that functionality). Then echo the field with some specific attributes:

**id** = $this->field['id']

**name** = $this->args['opt_name'][$this->field['id']]

**value** = $this->value

**span class="description"** = $this->field['desc'] - Not required, but usefull

You can also create any other options for that field type, if set in the theme-options array for that field they will be available in the $this->field array.


***


### Class Enqueue Function ###

Now lets take a look at the enqueue function.

{% highlight php %}
/**
 * Enqueue Function. (optional)
 *
 * If this field requires any scripts, or css define this function and register/enqueue the scripts/css
 *
 * @since NHP_Options 1.0
 */
function enqueue(){
        
    wp_enqueue_script(
        'nhp-opts-field-text-js',//unique name
        $this->args['theme_url'].'options/fields/text/field_text.js', //can be any url
    array('jquery', 'farbtastic'),//requires
    time(),//expires
    true//in footer
    );
        
}//function
{% endhighlight %}

This function is NOT required, but if you custom field needs to load css or js files, this is the easiest way to do so.
It **MUST** be called enqueue for it to be loaded, so make sure you spell it right :-).

Then simply enqueue your scripts / styles using the built in WordPress methods for enqueue'ing scripts/css.



Then you just need to wrap the class up, include it before calling the NHP_Options class and you can assign it to fields.

**NOTE** There is a hook point in the NHP Theme Options Framework which calles the field classes, so when including classes its a good idea to do it here like so:

{% highlight php %}
add_action('nhp-opts-get-fields', 'require_my_custom_field');
function require_my_custom_field(){
    require_once('pathtofield/field_example.php');
}//function
{% endhighlight %}
