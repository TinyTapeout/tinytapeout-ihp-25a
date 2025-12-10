<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## Overview

**For a quick-start guide just see the "How to test" heading below. I intend to have results collected in the [TTIHP25a-ring-osc2](https://docs.google.com/spreadsheets/d/1ijWdzJL9L4ZYqBhKCiZMeHCRW9pjFe_lTgYaaWa5nSQ/edit?gid=2103663522#gid=2103663522) sheet of my "Anton's Tiny Tapeout silicon testing" Google Sheet.**

There are 6 ring oscillators of various lengths in this design, ranging from 13 inverters up to 1001 inverters. 4 of them give their direct outputs. 4 also give their output divided by 16. 2 also drive PWM outputs at high frequency to see whether the output pins will filter them to "analog-like" waveforms, or whether instead the chip characteristics just kill the outputs.

This is implemented using the IHP SG13G2 open PDK and was fabricated on TTIHP25a, though it was originally intended for TT09.

Originally this project was submitted to TT09 (commit [ee2feec](https://github.com/algofoogle/tt09-ring-osc2/commit/ee2feec185f6f5ddf48dfbf057093a3cfc8f5dea)). It was later [rehardened](https://github.com/TinyTapeout/tt09-ttihp25a-reharden/tree/main/hdl/tt_um_algofoogle_tt09_ring_osc2) for resubmission to TTIHP25a (wherein some minor changes were required).

*See also: [tt09-ring-osc](https://github.com/algofoogle/tt09-ring-osc) and [tt09-ring-osc3](https://github.com/algofoogle/tt09-ring-osc3) for my other ring oscillator experiments on the same shuttle.*


## How to test

1.  Set `ui_in` to 0; this should configure all the PWM experiments to do nothing.
2.  Probe `uo_out[3]` (`ring_1001`) with an oscilloscope: This is the raw output of the longest (1001-inverter) ring oscillator.
3.  Probe through each of `uo_out[2:0]`: Each step to a lower bit is another ring that is half the length (and hence should be double the frequency): 501 inverters (`ring_501`), then 251 inverters (`ring_251`), then 125 inverters (`ring_125`).
4.  Probe `uo_out[4]` (`c0_3`): This is `ring_501` divided by 16.
5.  Probe `uo_out[5]` (`c1_3`): This is `ring_125` divided by 16.
6.  Probe `uo_out[6]` (`c2_5`): This is the much faster `ring_25` divided by 64.
7.  Probe `uo_out[7]` (`c3_5`): This is the fastest `ring_13` divided by 32 -- probably too fast (on the order of 120MHz?)
8.  Probe `uio_out[7,6,1]`: These are the PWM experiment outputs and all are expected to be at 0.
9.  Probe `uio_out[7,6,1]` while setting `ui_in` to each of:
    1.  `00100101`: 25% duty PWM for `uio_out[7]` and `uio_out[6]`, 12.5% duty for `uio_out[1]`.
    2.  `01001010`: 50% duty PWM for `uio_out[7]` and `uio_out[6]`, 25% duty for `uio_out[1]`.
    3.  `01101111`: 75% duty PWM for `uio_out[7]` and `uio_out[6]`, 37.5% duty for `uio_out[1]`.
    4.  `10000000`: 50% duty for `uio_out[1]`.
    5.  `10100000`: 62.5% duty for `uio_out[1]`.
    6.  `11000000`: 75%
    7.  `11100000`: 87.5%

The hope is that the PWM outputs are at a high enough frequency that the duty cycle will be somewhat filtered to give an analog-like output, though it's likely the chip's mux and other characteristics along the way (including the pad drivers) will just lead to outputs that are mostly noisy.

