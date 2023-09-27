[![hacs_badge](https://img.shields.io/badge/HACS-Default-41BDF5.svg)](https://github.com/custom-components/hacs)
![Version](https://img.shields.io/github/v/release/SirGoodenough/Logic-Chekr)

<a href="https://www.buymeacoffee.com/SirGoodenough"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=SirGoodenough&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" width=auto, height=30/></a>
<base target="_blank">

# Logic-Chekr

This Custom Template for checking if members of a list of entities such as input_booleans or binary_sensors or other custom sensors are displaying True or False. I found that the !input value of entities you typically get from a BluePrint is a list of entities, so constructs like is_state will not work with them directly. I came up with this to make that easier to manage. Of course bare entities can also be checked by putting them in as a [ ] braces list, so it works both ways.

Templates are available for testing both True and False separately, and you can check if any are that state, all are that state, or only one is that state. Items that are a state other than some of the standard [truthy/falsy](https://www.freecodecamp.org/news/truthy-and-falsy-values-in-python/) indications will be ignored. (null, unavailable, unknown, numbers that are not 0 or 1, etc.)

The main reason for using this template is not because it's complicated, it's because the logic check is something you may be using over and over when you are dealing with automations, so being able to repeat the same action over and over is better if there is 1 place in your project the code exists. If you are only going to use this template in one place in your code, just copy the template and paste it in there directly for simplicity.

# Installation

Install this in HACS or download the `logic_chekr.jinja` from this repository and place the files into your `config\custom_templates` directory.
[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=SirGoodenough&repository=Logic-Chekr&category=template)

#### If you cannot see templates in your HACS listing

You *may* need to enable 'experimental features' mode. To do this find the HACS section of the Home Assistant Integration page. Click on the '>' arrow to bring you to the custom integration page. Then click on configure, and select 'enable experimental features' check box. click submit, then float out and restart the HA server to make sure it takes. When you come back HACS will look slightly different, but the Templates section is now visible and you will be able to select it. At some point in time HACS will update and the new interface and options will be the only available interface.

*********************

# Test for ANY to be True

## `true_any([entity1, entity2, /])`

This expects a list of entities. This means [ ] braces OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the braces.

- The number of entities that evaluate as True using `bool(value, default) function` is counted.
      [truthy values](https://www.home-assistant.io/docs/configuration/templating/#numeric-functions-and-filters)
- Items that do not evaluate as bool will be defaulted to null/undefined.
- If there are one or more that match, True is returned, else False, defaults to False.

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

*********************

# Test for ANY to be False

## `false_any([entity1, entity2, /])`

This expects a list of entities. This means [ ] braces OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the braces.

- The number of entities that evaluate as False using `bool(value, default) function` is counted.
      [falsy values](https://www.home-assistant.io/docs/configuration/templating/#numeric-functions-and-filters)
- Items that do not evaluate as bool will be defaulted to null/undefined.
- If there are one or more that match, True is returned, else False, defaults to False.

### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to to help with the logic status of entities.

```jinja
- if: >-
    {% from 'logic_chekr.jinja' import false_any %}
    {{- false_any( [door_open] ) | bool -}} 
```

*********************

# Test for ONE to be True

## `true_one([entity1, entity2, /])`

This expects a list of entities. This means [ ] braces OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the braces.

- The number of entities that evaluate as True using `bool(value, default) function` is counted.
      [truthy values](https://www.home-assistant.io/docs/configuration/templating/#numeric-functions-and-filters)
- Items that do not evaluate as bool will be defaulted to null/undefined.
- If there is only one that matches, True is returned, else False, defaults to False.

### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to to help with the logic status of entities.

```jinja
- if: >-
    {% from 'logic_chekr.jinja' import true_one %}
    {{- true_one( [door_open] ) | bool -}} 
```

*********************

# Test for ALL to be True

## `true_all([entity1, entity2, /])`

This expects a list of entities. This means [ ] braces OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the braces.

- The number of entities are counted.
- The number of entities that evaluate as True using `bool(value, default) function` is counted.
      [truthy values](https://www.home-assistant.io/docs/configuration/templating/#numeric-functions-and-filters)
- Items that do not evaluate as bool will be defaulted to True.
- If the 2 counts are the same, True is returned, else False, defaults to False.

### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to to help with the logic status of entities.

```jinja
- if: >-
    {% from 'logic_chekr.jinja' import true_all %}
    {{- true_all( [door_open] ) | bool -}} 
```

*********************

# Test for ONE to be False

## `false_one([entity1, entity2, /])`

This expects a list of entities. This means [ ] braces OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the braces.

- The number of entities that evaluate as False using `bool(value, default) function` is counted.
      [falsy values](https://www.home-assistant.io/docs/configuration/templating/#numeric-functions-and-filters)
- Items that do not evaluate as bool will be defaulted to null/undefined.
- If there is only one that matches, True is returned, else False, defaults to False.

### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to to help with the logic status of entities.

```jinja
- if: >-
    {% from 'logic_chekr.jinja' import false_one %}
    {{- false_one( [door_open] ) | bool -}} 
```

*********************

# Test for ALL to be False

## `false_all([entity1, entity2, /])`

This expects a list of entities. This means [ ] braces OR if your entities are pulled from a BluePrint entity selector, that is already a list and you do not need the braces.

- The number of entities are counted.
- The number of entities that evaluate as False using `bool(value, default) function` is counted.
      [falsy values](https://www.home-assistant.io/docs/configuration/templating/#numeric-functions-and-filters)
- Items that do not evaluate as bool will be defaulted to False.
- If the 2 counts are the same, True is returned, else False, defaults to False.
  
### REMEMBER!!

> This always returns text, so cast to bool on the other end to be certain of the result.
>
> Use of the - character in the return template ensures no unwanted spacing is pulled back with your answer.

### Examples

Generically, this can be dropped into many templates to to help with the logic status of entities.

```jinja
- if: >-
    {% from 'logic_chekr.jinja' import false_all %}
    {{- false_all( [door_open] ) | bool -}} 
```

*********************

# Full Example in an actual BluePrint

Here is a full example that uses this.  It is part of a BluePrint showing the use of 2 of the functions. Notice that since `door_open` is a list from an !input entity selector, no [ ] braces are required.

```yaml
variables:
    # Convert !inputs to variables
  cooldown: !input cooldown
  door_open: !input door_entity

action:
- alias: Repeat the sequence UNTIL the door is closed
  repeat:
    sequence:
    - alias: This is the delay broke into 2 sec incr so it can be interrupted.
      repeat:
        while: >
          {% from 'logic_chekr.jinja' import true_any %}
          {{- true_any( door_open ) | bool and repeat.index < cooldown/2 -}}
        sequence:
          - delay: 00:00:02
    - alias: Send announcement message (potentially again)
      if: >
        {% from 'logic_chekr.jinja' import true_any %}
        {{- true_any( door_open ) | bool -}}
      then:
      - service: tts.cloud_say
        data:
          entity_id: !input speaker_target
          message: !input announcement_message
          options:
            gender: !input speaker_gender
            voice: !input speaker_voice
          language: !input speaker_language
      - alias: Delay to make sure the message can complete.
        delay: 00:00:10
    until: >
       {% from 'logic_chekr.jinja' import false_all %}
       {{- false_all( door_open ) | bool -}}

```

*********************

# Other Info

Location of this code: https://github.com/SirGoodenough/Logic-Chekr

Let me know if you have a suggestion.

If you have any questions, comments or additions be sure to add an issue in the above listed github repo and bring them up on my Discord Server:

### 🤹🏾‍♂️ Contact Links or see my other work

What are we Fixing Today Homepage / Website: https://www.WhatAreWeFixing.Today/

Channel Link URL: (WhatAreWeFixingToday): https://bit.ly/WhatAreWeFixingTodaysYT

What are we Fixing Today Facebook page (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodaybFB

What are we Fixing Today X Account (Sir GoodEnough): https://bit.ly/WhatAreWeFixingTodayTW

Discord Guild: (Sir_Goodenough#9683): https://discord.gg/Uhmhu3B

BluePrint Library: https://github.com/SirGoodenough/HA_Blueprints/blob/master/README.md

#WhatAreWeFixingToday

#SirGoodEnough

### Disclaimer

⚠️ **DANGER OF ELECTROCUTION** ⚠️

If your device connects to mains electricity (AC power) there is danger of electrocution if not installed properly. If you don't know how to install it, please call an electrician (***Beware:*** certain countries prohibit installation without a licensed electrician present). Remember: **SAFETY FIRST**. It is not worth the risk to yourself, your family and your home if you don't know exactly what you are doing. Never tinker or try to flash a device using the serial programming interface while it is connected to MAINS ELECTRICITY (AC power).
