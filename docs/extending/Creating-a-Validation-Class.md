---
layout: page
title: Creating a Validation Class
category: Documentation
group: Extending the Framework
tags:
---

Creating a Custom Validation Class for the Theme Options Framework, it quite simple. There are multiple Validation Classes already, so taking a look at these can help to understand the proccess. These are located in the **options/validation** folder like so: **/options/validation/email/validation_name.php**

Lets take a look at a custom validation class, for this example we are going to look at a basic example validation class, the email validation class.

This is what the code the code looks like in the **/options/validation/email/validation_email.php** file

{% highlight php %}
<?php
class NHP_Validation_email extends NHP_Options{ 
    
    /**
     * Field Constructor.
     *
     * Required - must call the parent constructor, then assign field and value to vars, and obviously call the validate field function
     *
     * @since NHP_Options 1.0
    */
    function __construct($field, $value, $current){
        
        parent::__construct();
        $this->field = $field;
        $this->field['msg'] = (isset($this->field['msg']))?$this->field['msg']:__('You must provide a valid email for this option.', 'nhp-opts');
        $this->value = $value;
        $this->current = $current;
        $this->validate();
        
    }//function
    
    
    
    /**
     * Field Validate Function.
     *
     * Takes the vars and validates the value then optionaliy sets an error msg
     *
     * @since NHP_Options 1.0
    */
    function validate(){
        
        if(!is_email($this->value)){
            $this->value = (isset($this->current))?$this->current:'';
            $this->error = $this->field;
        }
        
    }//function
    
}//class
?>
{% endhighlight %}

Okay, lets break it down a little.

### Class Definition ###

Firstly we need to take note of defining the class and name:

{% highlight php %}
NHP_Validation_email extends NHP_Options
{% endhighlight %}

The NHP Theme Options Framework uses a naming structure for validation classes, so you **MUST** make sure you name custom classes like so:

{% highlight php %}
NHP_Validation_classname extends NHP_Options
{% endhighlight %}

When calling the custom validation class for a field in the theme options you would define the validate as myclassname

So a custom class called "example" would be declared like so:

{% highlight php %}
NHP_Validation_example extends NHP_Options
{% endhighlight %}

### Class Constructor ###

Now lets take a look at the classes constructor (required)

{% highlight php %}
<?php
/**
 * Field Constructor.
 *
 * Required - must call the parent constructor, then assign field and value to vars, and obviously call the validate field function
 *
 * @since NHP_Options 1.0
 */
function __construct($field, $value, $current){
        
    parent::__construct();
    $this->field = $field;
    $this->field['msg'] = __('You must provide a valid email for this option.', 'nhp-opts');
    $this->value = $value;
    $this->current = $current;
    $this->validate();
        
}//function
{% endhighlight %}

Here we need to call the parent class constructor so we can use the defined options

{% highlight php %}
parent::__construct();
{% endhighlight %}

Then we assign the passed vars **$field** (array from theme-options.php file), **$value** (the new value input by the user), **$current** (the current value in the database).

We also need to set the error message should the value be invalid and no custom message assigned, which is done by setting **$this->field['msg']**

{% highlight php %}
<?php
$this->field = $field;
$this->field['msg'] = (isset($this->field['msg']))?$this->field['msg']:__('You must provide a valid email for this option.', 'nhp-opts');
$this->value = $value;
$this->current = $current;
{% endhighlight %}

Then we need to call the **validate();** function, this will check the $this->value var and if it doesnt validate set the error flag and overwrite the value with the one currently set in the database. You can also optionally, or instead of setting an error, set a warning, which has the same functionality of error messages, but provides a different importance state to the user.

{% highlight php %}
<?php
/**
* Field Validate Function.
*
* Takes the vars and check the value, if incorrect reset to the current value in DB
*
* @since NHP_Options 1.0
*/
function validate(){

    if(!is_email($this->value)){
        $this->value = (isset($this->current))?$this->current:'';
        $this->error = $this->field;
        /*
         * Optionally set a warning, just like settings errors
         */
        //$this->warning = $this=>field;
    }//if

}//function
{% endhighlight %}

And thats it, if the value is okay the function doesn't need to assign anything, it just needs to check for an error and validate if there is.

**NOTE** There is a hook point in the NHP Theme Options Framework which calls the validate classes, so when including classes its a good idea to do it here like so:

{% highlight php %}
<?php
add_action('nhp-opts-get-validation', 'require_my_custom_validation');
function require_my_custom_validation(){
    require_once('pathtovalidationclass/validation_example.php');
}//function
{% endhighlight %}

**ANOTHER NOTE** Some validation classes like **html | no_html | js** dont need to set errors, they just need to filter the content, so they WILL override the current value ALWAYS. As an example here is the validate function for escaping JS.

{% highlight php %}
<?php
/**
 * Field Render Function.
 *
 * Takes the vars and validates them
 *
 * @since NHP_Options 1.0
 */
function validate(){

    $this->value = esc_js($this->value);
    
}//function
{% endhighlight %}
