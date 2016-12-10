# Custom Inputfield Dependencies

A module for ProcessWire CMS/CMF. Extends inputfield dependencies so that inputfield visibility or required status may be determined at runtime by custom PHP/API code. Requires the Hanna Code module.

## Overview

Custom Inputfield Dependencies uses the Hanna Code module as a convenient way to execute any arbitrary PHP/API code at runtime. The idea is that you create Hanna Code tags that echo some result that you want to make an inputfield dependent on. The $page variable in your Hanna tag code will refer the page being edited.

For each Hanna tag selected in Custom Inputfield Dependencies a hidden inputfield will be added to Page Edit for the connected template - the hidden inputfield is named the same as the Hanna tag and its value is the result of the Hanna tag. This allows other inputfields to be made dependent on the value of the hidden inputfield.

Note that the value of the hidden inputfield is only calculated once at the time Page Edit loads - if your Hanna tag code refers to fields in the page being edited then changes will not be recalculated until the page is saved and Page Edit reloaded.

The name of Hanna tags that you want to use with Custom Inputfield Dependencies must start with an underscore.

## Example

Take an example: I want site editors to type some summary text and select a representative image for pages using the basic_page template. The summary text/image will be used to create feature boxes on parent pages that link to the children. So I don't need editors to fill out these fields on top-level pages directly below the Home page, but only for pages at level 2 or deeper. So I create a Hanna tag "_parents_count":

`<?php
echo $page->parents->count();`

I connect this Hanna tag with the basic_page template in the Custom Inputfield Dependencies module config.

Now I can create show-if and require-if dependencies for my summary fields so they are only shown and required for pages at level 2 or deeper:

`_parents_count>1`

## Usage

1. [Install](http://modules.processwire.com/install-uninstall/) the Custom Inputfield Dependencies module.

2. Create one or more Hanna tags that echo a result that you will make an inputfield dependent on. The name of Hanna tags that you want to use with Custom Inputfield Dependencies must start with an underscore. 
 
3. Fill out the Custom Inputfield Dependencies module config according to your needs:

* Template: the template that contains the inputfield you want to create a custom dependency for.
* Hanna tag that echos field value: a Hanna tag that you created previously for the purpose.
* You can add rows as needed using the "Add another row" button.
* Debug mode: normally the results of the selected Hanna tags are hidden in Page Edit, but you can check "Debug mode" to show the fields and check what the Hanna tags are returning.

## License

Released under Mozilla Public License v2. See file LICENSE for details.
