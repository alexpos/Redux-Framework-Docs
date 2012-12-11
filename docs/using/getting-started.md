---
category: Documentation
status: wip
group: Using the Framework
title: "Getting Started with Redux"
tags: 
layout: page
---

The Redux Framework is hosted on Github. There are two ways to add the Redux Framework into your WordPress theme: Using a git-submodule, or copying the framework-folder. Let's strat with the recommended way.

###Working with a Git Submodule (recommended)

If you use git to develop your theme (if not, why not!?), then using a submodue is the way to go. This makes it easy for you to stay up-to-date with the latest version of the Redux Framework. Any time we update the module, you can run ```git submodule update``` and grab the latest stable version of the framework from [the repository][red].

[red]: https://github.com/ghost1227/Redux-Framework

This is how to install Redux using git submodule:

    $ cd your-theme/whatever-folder
    $ git submodule add https://github.com/ghost1227/Redux-Framework git what-ever-name

The alternative is adding the framework to your theme and updating by hand.

###Simply use the zip-file

Download the [Remux Framework as a ZIP file here]( {{ site.download }} ), unzip it, and then move the options-folder somewhere in your  theme. The options-folder under admin is the only folder we actually need. Options.php is a demo file, we will use that file next.

    $ tree -L 3 Remux-Framework/
    Remux-Framework/
    ├── README.md
    ├── admin
    │   ├── options
    │   │   ├── css
    │   │   ├── fields
    │   │   ├── img
    │   │   ├── js
    │   │   ├── options.php
    │   │   └── validation
    │   └── options.php
    └── redux-framework.php

##Test the framework

The framework comes with a demo-file that contains everything the theme can do. It is the easiest way to get to know the framework, and see how the options are used.

Call the options file from your ```functions.php```

    include_once('Redux-Framework/admin/options.php');

Change this so it fits your location. Have fun looking around!

<div class="row-fluid">
    <ul class="thumbnails">
      <li class="span4">
        <div class="thumbnail">
          <a class="fancybox" rel="gallery" href="{{ site.base_dir }}/img/shots/9-Redux-Dev-Mode.png" title="Framework Dev Mode Section"><img alt="" src="{{ site.base_dir }}/img/shots/thumbs/9-Redux-Dev-Mode.png"></a>
          <h4>Dev Mode Info</h4>
          <p>Setting dev mode to true allows you to view the class settings/info in the panel.</p>
        </div>
      </li>
      <li class="span4">
        <div class="thumbnail">
          <a class="fancybox" rel="gallery" href="{{ site.base_dir }}/img/shots/7-Redux-Docs.png" title="Framework Dev Mode Section"><img alt="" src="{{ site.base_dir }}/img/shots/thumbs/7-Redux-Docs.png"></a>
          <h4>Documentation</h4>
          <p>Set ANY custom page help tabs, displayed using the new help tab API. Tabs are shown in order of definition.</p>
        </div>
      </li>
      <li class="span4">
        <div class="thumbnail">
          <a class="fancybox" rel="gallery" href="{{ site.base_dir }}/img/shots/6-Redux-Import-Export.png" title="Framework Dev Mode Section"><img alt="" src="{{ site.base_dir }}/img/shots/thumbs/6-Redux-Import-Export.png"></a>
          <h4>Import / Export Options</h4>
          <p>Enable / Disable the export functionality</p>
        </div>
      </li>
    </ul>
</div>



##Start using the framework in your theme

The fastest way to start using the framework in your theme is to copy Redux-Framework/admin/options.php to theme-options.php, and include this file in your ```functions.php```

    if( file_exists(get_template_directory().'/theme-options.php') )
        include_once(get_template_directory().'/theme-options.php');

###Configure it for your theme

Opening the file, let's see what we can change.

If you are running on Windows you may have URL problems which can be fixed by defining the framework url first. Comment out the line:

    //define('Redux_OPTIONS_URL', site_url('path the options folder'));

and set it to the currect url. If you are using a child-theme, then this snippet might help:

    if( function_exists( 'wp_get_theme' ) ) {
        if( is_child_theme() ) {
            define('Redux_OPTIONS_URL', get_stylesheet_directory_uri().'/admin/options/');
        } else {
            define('Redux_OPTIONS_URL', get_template_directory_uri().'/admin/options/');
        }
    }

The demo-file is commented well, and is the main documentation to create your own theme options.

##Walking through setup\_framework\_options()

These are the main options that change how the framework behaves. All these settings can also be found in ```options.php```.

Setting dev mode to true allows you to view the class settings/info in the panel. (Default is false)

    $args['dev_mode'] = true;

If you want to use Google Fonts, you have to set your api-key (you can [get one here][gfo]).

    $args['google_api_key'] = 'your-key';

[gfo]: https://code.google.com/apis/console/

You can set the default tab to open

    $args['last_tab'] = '0';

You can override the css-file for the menu

    $args['admin_stylesheet'] = 'standard';

You can set it to: *standard* (do nothing), *custom* (make some small chnages, don't overwrite them on update! Custom is located in options/css, and last *none*, which disable Redux to use css, so you must supply your own.

The form can be styled with the following keys:

    $args['intro_text']

This text is displayed above the options panel. The intro_text field accepts all HTML.

    $args['footer_text']

This text is displayed below the options panel. Also accepts all HTML.
    $args['footer_credit']

This text is displayed in the options panel footer across from the WordPress version (where it normally says \'Thank you for creating with WordPress\'). This field accepts all HTML.

Next you can setup some links in the footer:

    $args['share_icons']['twitter']
    $args['share_icons']['linked_in']

You can add other social services, or links if you want, just use ```share_icons```.

Enable / Disable the export functionality:

    $args['show_import_export'] = false;

Custom option name, change this, for example, the name of your theme:

    $args['opt_name'] = 'twenty_eleven2';

A custom icon gives your theme a professional look:

       $args['menu_icon'] = '';

Next you can change the page-title, menu-title and slug for the options page (wp-admin/themes.php?page=myslug):

    $args['menu_title'] = __('Options', Redux_TEXT_DOMAIN);
    $args['page_title'] = __('Options', Redux_TEXT_DOMAIN);
    $args['page_slug'] = 'redux_options';

Page capabilities

    $args['page_cap'] = 'manage_options';

Set up the menu. The menu type (set to "menu" for a top level menu, or "submenu" to add below an existing item). Set the parent menu (see http://codex.wordpress.org/Function_Reference/add_submenu_page#Parameters). Set a custom page location. This allows you to place your menu where you want in the menu order. Must be unique or it will override other items!

    $args['page_type'] = 'submenu';
    $args['page_parent'] = 'options_general.php';
    $args['page_position'] = null;

And two more settings for the menu. Set a custom page icon class (used to override the page icon next to heading). And disable the panel sections showing as submenu items.

    $args['page_icon'] = 'icon-themes';
    $args['allow_sub_menu'] = false;

Set ANY custom page help tabs, displayed using the new [help tab API](http://codex.wordpress.org/Function_Reference/add_help_tab). Tabs are shown in order of definition.

    $args['help_tabs'][] = array()
    $args['help_sidebar']  = array()

