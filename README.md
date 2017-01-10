# Custom Inputfield Dependencies

A module for ProcessWire CMS/CMF. Extends inputfield dependencies so that inputfield visibility or required status may be determined at runtime by selector or custom PHP code.

## Overview

Custom Inputfield Dependencies adds several new settings options to the "Input" tab of "Edit Field". These are described below.

Note that the visibility or required status of fields determined by the module is calculated once at the time Page Edit loads. If your dependency settings refer to fields in the page being edited then changes will not be recalculated until the page is saved and Page Edit reloaded.

## Usage

[Install](http://modules.processwire.com/install-uninstall/) the Custom Inputfield Dependencies module.

Optional: for nice code highlighting of custom PHP install [InputfieldAceExtended](http://modules.processwire.com/modules/inputfield-ace-extended/) v1.2.0 or newer (currently available on the ['dev' branch](https://github.com/owzim/pw-inputfield-ace-extended/tree/dev) of the GitHub repo).

The custom inputfield dependencies are set on the "Input" tab of "Edit Field".

!['Visibility' settings](https://raw.githubusercontent.com/Toutouwai/CustomInputfieldDependencies/master/img/visibility.png)

!['Required' settings](https://raw.githubusercontent.com/Toutouwai/CustomInputfieldDependencies/master/img/required.png)

###Visibility

####Show only if page is matched by custom find

Use InputfieldSelector to create a $pages->find() query. If the edited page is matched by the selector then the field is shown.

![Custom find settings](https://raw.githubusercontent.com/Toutouwai/CustomInputfieldDependencies/master/img/custom-find.png)

####Show only if page is matched by selector

As above, but the selector string may be entered manually.

![Selector string settings](https://raw.githubusercontent.com/Toutouwai/CustomInputfieldDependencies/master/img/selector-string.png)

####Show only if custom PHP returns true

Enter custom PHP/API code – if the statement **returns boolean true** then the field is shown. `$page` and `$pages` are available as local variables – other API variables may be accessed with `$this`, e.g. `$this->config`

![Custom PHP settings](https://raw.githubusercontent.com/Toutouwai/CustomInputfieldDependencies/master/img/custom-php.png)

In most cases `$page` refers to the page being edited, but note that if the field is inside a repeater then `$page` will be the repeater page. As there could conceivably be cases where you want to use the repeater page in your custom PHP the module does not forcibly set `$page` to be the edited page. Instead, a helper function `getEditedPage($page)` is available if you want to get the edited page regardless of if the field in inside a repeater or not.

    $edited_page = $this->getEditedPage($page);

###Required

The settings inputfields are the same as for Visibility above, but are used to determine if the field has 'required' status on the page being edited.

## License

Released under Mozilla Public License v2. See file LICENSE for details.
