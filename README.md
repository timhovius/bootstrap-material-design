[![build status](https://travis-ci.org/FezVrasta/bootstrap-material-design.svg?branch=master)](https://travis-ci.org/FezVrasta/bootstrap-material-design)

[![banner](https://github.com/FezVrasta/bootstrap-material-design/raw/master/demo/imgs/banner.jpg)](#)

This Bootstrap theme is an easy way to use the new [Material Design guidelines by Google](http://www.google.com/design/spec/material-design/introduction.html) in your Symfony2 application.

**NOTE**: This theme is still in development, it could be used on production websites but I can't guarantee compatibility with previous versions.

Check out [the demo at this link](http://fezvrasta.github.io/bootstrap-material-design/).

## How to install

Add the folowing line to your composer.json file: `"timhovius/bootstrap-material-design": "dev-master"`  
Run `php composer.phar install` and the bundle can be used now.

###Bonus
If you want to use this bundle with the BraincraftedBootstrapBundle, you have to add the following lines to your `config.yml`:

    # Assetic Confguration
    ...
    assets:
        bootstrap_css:
            inputs:
                - %kernel.root_dir%/../vendor/twbs/bootstrap/less/bootstrap.less
                - %kernel.root_dir%/../vendor/timhovius/bootstrap-material-design/less/ripples.less
                - %kernel.root_dir%/../vendor/timhovius/bootstrap-material-design/less/material.less
                - %kernel.root_dir%/../vendor/braincrafted/bootstrap-bundle/Braincrafted/Bundle/BootstrapBundle/Resources/less/form.less
            filters:
                - less
                - cssrewrite
            output: css/material.css
        bootstrap_js:
            inputs:
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/transition.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/alert.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/button.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/carousel.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/collapse.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/dropdown.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/modal.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/tooltip.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/popover.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/scrollspy.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/tab.js
                - %kernel.root_dir%/../vendor/twbs/bootstrap/js/affix.js
                - %kernel.root_dir%/../vendor/timhovius/bootstrap-material-design/scripts/ripples.js
                - %kernel.root_dir%/../vendor/timhovius/bootstrap-material-design/scripts/material.js
                - %kernel.root_dir%/../vendor/braincrafted/bootstrap-bundle/Braincrafted/Bundle/BootstrapBundle/Resources/js/bc-bootstrap-collection.js
            output: js/material.js

And in the `braincrafted_bootstrap` section you have to set `assetic` to `false` and set the `assets_dir` to the `bootstrap-material-design` folder.

    braincrafted_bootstrap:
        ...
        assets_dir: %kernel.root_dir%/../vendor/timhovius/bootstrap-material-design
        ...
        auto_configure:
            assetic: false
            ...

You can use the basic template from the BraincraftedBootstrapBundle to include the CSS and JavaScript files:

    <!DOCTYPE html>
    <html>
    <head>
    
        <title>Bootstrap 101 Template</title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- Bootstrap -->
        <link href="{{ asset('css/material.css') }}" rel="stylesheet" media="screen">
    
        <!-- HTML5 Shim and Respond.js add IE8 support of HTML5 elements and media queries -->
        {% include 'BraincraftedBootstrapBundle::ie8-support.html.twig' %}
    
    </head>
    
    <body>
        <h1>Hello, world!</h1>
    
        <!-- jQuery (necessary for Bootstraps JavaScript plugins) -->
        <script src="{{ asset('js/jquery.js') }}"></script>
        <!-- Include all JavaScripts, compiled by Assetic -->
        <script src="{{ asset('js/material.js') }}"></script>
        <!-- Enable Android effects -->
        <script>
            $(function() {
                $.material.init();
            });
        </script>
    </body>
    </html>

#### material-wfont.less or material.less?

The only difference is that `material-wfont.less` has the Google web fonts included.

# Documentation

Material Design for Bootstrap provides some additional stuff to get the best from Material Design.

### Variations

There are 17 additional color variations (in addition to the classic 4 variations) for buttons, inputs, checkboxes, radios, alerts, navbars, tabs, labels, paginations, progress bars and more.
They can be used by adding the class suffix `-material-color` to the desired element and replacing `color` with the desired one.

Example:

    <button class="btn btn-material-deep-purple">Deep purple button</button>

These colors are taken from the Material Design color palette and are reported below:

![palette](demo/imgs/palette.jpg)

### Buttons

Add `.btn-flat` to a button to make it flat, without shadows.
Add `.btn-raised` to a button to add a permanent shadow to it.

### Inputs

Add `.floating-label` to an input field with a `placeholder` to transform the placeholder in a floating label.

Add `data-hint="some hint"` to show an hint under the input when the user focus it.

Remember to use the proper HTML markup to get radio and checkboxes styled correctly (choose between *radio* or *checkbox*):

    <div class="radio/checkbox radio-primary">
        <label>
            <input type="radio/checkbox" checked>
            Option one is this
        </label>
    </div>

### Icons

Material Design for Bootstrap includes 490 original Material Design icons!
These icons are extracted from the original Google sources and are licensed under the BSD license.
They are provided as an iconic and easy to use font.

Variations are available for every icon, including the original Bootstrap icons.

The syntax to add a Material icon is:

     <i class="icon icon-material-favorite"></i>

## Material.js

`Material.js` is a jQuery plugin that adds some magic to your markup and allows Material Design for Bootstrap to style some elements like inputs, checkboxes, radios etc.

### Functions

* `$.material.init()` - shortcut to run all the following commands:
* `$.material.ripples()` will apply ripples.js to the default elements.
* `$.material.input()` will enable the MD style to the text inputs, and other kind of inputs (number, email, file etc).
* `$.material.checkbox():` will enable the MD style to the checkboxes (remember to follow the markup guidelines explained in the [Inputs section](#inputs).
* `$.material.radio():` will enable the MD style to the checkboxes (remember to follow the markup guidelines explained in the Inputs section.

### Apply Material.js only to specific elements

Every function expects an optional value that will be used as a selector for the function; for example,
`$.material.ripples("#selector, #foobar")` will apply Ripples.js only to `#selector` and `#foobar`.
The functions that allows an optional selector are `$.material.ripples`, `$.material.input`, `$.material.checkbox` and `$.material.radio`.

You can even override the default values using the `$.material.options` function. The default values are:

    $.material.options = {
        "withRipples": ".btn:not(.btn-link), .card-image, .navbar a:not(.withoutripple), .nav-tabs a:not(.withoutripple), .withripple",
        "inputElements": "input.form-control, textarea.form-control, select.form-control",
        "checkboxElements": ".checkbox > label > input[type=checkbox]",
        "radioElements": ".radio > label > input[type=radio]"
    }

### Arrive.js support

If you need to dynamically add elements to your DOM then you may need to include `Arrive.js` before `Material.js`. This will automatically apply `Material.js` to every new element added via JavaScript.

## Plugins

Material Design for Bootstrap comes with styling support for various external scripts:

### SnackbarJS

Create snackbars and toasts with the [SnackbarJS plugin](https://github.com/FezVrasta/snackbarjs). The default toast style is the squared one (snackbar style). If you like to use the rounded style (toast style), please add the `toast` class to the `style` option of SnackbarJS.

### RipplesJS

This is part of the Material Design for Bootstrap project and is a plain JavaScript script which creates the ripple effect when clicking on the specified elements.
At the moment RipplesJS does not have its own repository but it will probably have one in the future.

You may want to set a custom color to the ripples of a specific element, to do so write:

    <button class="btn btn-default" data-ripple-color="#F0F0F0">Custom ripple</button>

### noUiSlider

Make cross-browser sliders and get them styled with Material Design thanks to the support provided by this theme.
Read more about [noUiSlider here](http://refreshless.com/nouislider/).

### Dropdown.js

Finally a dropdown plugin that transforms select inputs in nice dropdowns and does not drive you crazy.
Read more about [Dropdown.js here](https://github.com/FezVrasta/dropdown.js).

### Selectize.js

Transform select and multi-select inputs into advanced text inputs. Material Design for BS provides a full replacement of the plugin's CSS, so don't include it.
Read more about [selectize.js](http://brianreavis.github.io/selectize.js/).

## Compatibility

Currently, Material Design for Bootstrap supports Google Chrome (tested v37+), Mozilla Firefox (tested 30+), and Internet Explorer (tested 11+). Mobile browsers are not currently tested but they may work.
