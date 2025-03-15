<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

It's a simple project done in WokWi during a workshop. You give it clock, it shows you a snake on a 7-segment indicator. No reset logic unfortunately, initial state is unpredictable.

## How to test

Supply clock over a pin. There is no debounce logic, so using a physical button will not work properly.

## External hardware

7-segment indicator, dot is not used.
