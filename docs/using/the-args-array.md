---
layout: page
title: The $args array
category: Documentation
group: Using the Framework
tags:
---

The $args array is the configuration array for setting up the Framework class.

By default this doesn't need to be passed to the class like the $sections array. It has its values set by default. But as this Framework is designed to be extendable it can be over written with your own preferences.

A working example of the attributes is included in the **theme-options.php** file for you to see, but we're are going to look through the settings below.

Each attribute is an element in the array $args, and is passed as the second parameter when calling the class, like so:

{% highlight php %}
<?php
new NHP_Options($sections, $args);
?>
{% endhighlight %}

So let's take a look at the attributes.   

{% highlight php %}
$args['opt_name'] = 'custom_option_name';
{% endhighlight %}

This attribute allows you to override the default option name, which is the theme name in lower case with spaces replaced with underscores (ie, twenty_eleven).
This must not contain any special characters and must have no spaces.

***


{% highlight php %}
$args['page_slug'] = 'custom_page_slug';
{% endhighlight %}

This attribute allows you to override the default page slug, which is "nhp\_theme\_options". And is displayed after **theme.php?page=**.
Again this must be special character free and have no spaces.   



***


{% highlight php %}
$args['page_title'] = 'Theme Options';
{% endhighlight %}

This attribute allows you to override the default page title, which is "Theme Options".   



***


{% highlight php %}
$args['page_cap'] = 'manage_options';
{% endhighlight %}

This attribute allows you to set the pages access rights, which by default is "manage_options".   



***


{% highlight php %}
$args['menu_title'] = 'Theme Options';
{% endhighlight %}

This is the menu name for the page, which by default is "Theme Options".   



***


{% highlight php %}
$args['dev_mode'] = true;
{% endhighlight %}

This will enable the "dev mode" tab in the sidebar of the panel, use it to view the Framework object when creating your options. Default is false and its advised to keep it that way when releasing the theme.   



***


{% highlight php %}
$args['stylesheet_override'] = true;
{% endhighlight %}

If you want to completely remove the default stylesheet and enqueue your own, set this to "true" and it will stop the default one being called.   



***


{% highlight php %}
$args['intro_text'] = __('<p>HTML allowed</p>', 'nhp-opts');
{% endhighlight %}

This attribute will insert content before the options panel, HTML is allowed.   



***


{% highlight php %}
$args['support_url'] = 'http://no-half-pixels.com';
{% endhighlight %}

If you want a tab/link for support you need to define this arg with the URL you want it to point to.   



***


{% highlight php %}
$args['share_icons']['twitter'] = array('link' => 'link url','title' => 'Folow me on Twitter', 'img' => 'img url');
{% endhighlight %}

The "share" section is displayed in the options panel footer, here you can create links to your sites/profiles. You need to define the link, title, and img url in the array. And you can create as many of these as you like (within reason). Best images are square 24px by 24px.   



***


{% highlight php %}
$args['show_theme_info'] = false;
{% endhighlight %}

Set this to false to stop the Theme Information tab from being displayed - default functionality is to allow.   



***


{% highlight php %}
$args['show_import_export'] = false;
{% endhighlight %}

Choose to disable the Import / Export Feature of the Framework.   



***


{% highlight php %}
$args['help_sidebar'] = __('<p>This is the sidebar content, HTML is allowed.</p>', 'nhp-opts');
{% endhighlight %}

Here you can define the Help tab sidebar (not set by default). HTML is allowed here.   



***

        
{% highlight php %}
$args['help_tabs'][] = array('id' => 'nhp-opts-1','title' => __('Theme Information 1', 'nhp-opts'),'content' => __('<p>This is the tab content, HTML is allowed.</p>', 'nhp-opts'));
{% endhighlight %}

The help\_tabs attribute allows you to define multiple help tabs for use on the theme options page. Simply assign a new array to the main help\_tabs array to create a new tab.   
