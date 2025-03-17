<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

"This project is a 4-bit synchronous counter with a fully-decoded hex output. An enable input is provided

Decoding is done entirely with 29 2-input NAND gates, following the insanely minimized design from Kim Oyhus
in the code golf stack exchange. One gate was trivially elminated because the complementary input was
available. Possibly further optimization would be possible since it was not optimized for this particular
situation. There are many gate delays between the input chanage and the last output change, however
that is deemed insignificant for a display application. 
"

## How to test

"Reset will reset the counter to 0 asynchronously, so the display will show '0'
 IN0 is enable (active high). To get the counter to count make IN0 high
 The counter counts on the positive edge of the clock input. 
 Fully decoded 7-segment (active high) is provided on outputs 0..6. Output 7 is not used. 


" 

## External hardware

"No external hardware is required beyond the standard demo board"
![kim_solution](https://github.com/user-attachments/assets/dd6803ec-c1c2-43b0-928c-e148c7fe08c3)
