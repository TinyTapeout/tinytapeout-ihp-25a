<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This module is capturing high edges in input lines (triggers) and stores the timestamp when this happened.
Period of internal counter is order of 30ms (24b).

Main clk is used for intetrnal logic and timestamp timer.
When edge on trigger input is detected, time is captured (max capture frequency is clk/2, but preferably even lower).

When data to read is available it is signalled on data reayd output pin.

In order to read the data, first set high enable pin, hold it and while holding start clocking data clk input.
(max data clk rate should be over 2 times slower than clk).
Read the data on output pin on data clk rising edge. 3 bytes should be read. Most significant bit is transferred first.

## How to test

Just hope that this works (tested maually on simulator exactly once..)

## External hardware

None, but signal generator bursting a few edges into trig input might be helpful
