[![hacs_badge](https://img.shields.io/badge/HACS-Default-41BDF5.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/SirGoodenough/Logic-Chekr)

<a href="https://www.buymeacoffee.com/SirGoodenough"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=SirGoodenough&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" width=auto, height=30/></a>
<base target="_blank">

# Logic-Chekr

This Custom Template for checking if members of a list of entities such as input_booleans or binary_sensors or other custom sensors are displaying True or False. I found that the !input value of entities you typically get from a BluePrint is a list of entities, so constructs like is_state will not work with them directly. I came up with this to make that easier to manage. Of course bare entities can also be checked by putting them in as a [] bracket list, so it works both ways.

Templates are available for testing both True and False separately, and you can check if Any are that state, all are that state, or only one is that state. Items that are a state other than some of the standard True/False indications will be ignored. (unavailable, unknown, etc)

The main reason for using this template is not because it's complicated, it's because the logic check is something you may be using over and over when you are dealing with automations, so being able to repeat the same action over and over is better if there is 1 place in your project the code exists.

# Installation

Install this in HACS or download the `logic_chekr.jinja` from this repository and place the files into your `config\custom_templates` directory.
[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=SirGoodenough&repository=Logic-Chekr&category=template)

If you cannot see templates in your HACS listing, you *may* need to enable 'experimental features' mode. To do this find the HACS section of the Home Assistant Integration page. Click on the '>' arrow to bring you to the custom integration page. Then click on configure, and select 'enable experimental features' check box. click submit, then float out and restart the HA server to make sure it takes. When you come back HACS will look slightly different, but the Templates section is now visible and you will be able to select it. At some point in time HACS will update and the new interface and options will be the only available interface.

# Test for ANY to be True

## `true_any([entity1, ...])`

This expects a list of entities. This means [] brackets OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the brackets.

- The number of entities are counted.
- The number of entities that are one of: ['true','True','yes','Yes','YES','on','ON','t','T','y','Y'] is counted.
- If there are one or more that match, true is returned, else false, defaults to false.

### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to to help with the logic status of entities.

```jinja
- if: >-
    {% from 'logic_chekr.jinja' import true_any %}
    {{- true_any( [door_open] ) | bool -}} 
```








Here is a full example that uses this.  It will give you percent sunshine estimate based on data from sun angle and cloud coverage if you have those integrations in your config. (Found the state statement somewhere a while ago, sorry there is no attribution. I use it in my personal config.)

```jinja
TBD

```

### Other Info

Location of this code: https://github.com/SirGoodenough/Availability-Template

Let me know if you have a suggestion.

If you have any questions, comments or additions be sure to add an issue in the above listed github repo and bring them up on my Discord Server:

### 🤹🏾‍♂️ Contact Links or see my other work

What are we Fixing Today Homepage / Website: https://www.WhatAreWeFixing.Today/

Channel Link URL: (WhatAreWeFixingToday): https://bit.ly/WhatAreWeFixingTodaysYT

What are we Fixing Today Facebook page (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodaybFB

What are we Fixing Today Twitter Account (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodayTW

Discord Guild: (Sir_Goodenough#9683): https://discord.gg/Uhmhu3B

BluePrint Library: https://github.com/SirGoodenough/HA_Blueprints/blob/master/README.md

#WhatAreWeFixingToday

#SirGoodEnough

### Disclaimer

⚠️ **DANGER OF ELECTROCUTION** ⚠️

If your device connects to mains electricity (AC power) there is danger of electrocution if not installed properly. If you don't know how to install it, please call an electrician (***Beware:*** certain countries prohibit installation without a licensed electrician present). Remember: _**SAFETY FIRST**_. It is not worth the risk to yourself, your family and your home if you don't know exactly what you are doing. Never tinker or try to flash a device using the serial programming interface while it is connected to MAINS ELECTRICITY (AC power).
