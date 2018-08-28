FPGA
===

[TOC]

## Look Up Table (LUT) in FPGA
{%youtube Usoo2j2TQio %}

## Flip-Flip (register) in FPGA
{%youtube lrXjuotxqzE %}


## Timing constrain of Flip-Flop
{%youtube WNZKu7anl2k %}

 - Set up time: 
     - The time before rising edge of the clk that the input signal must not change
     - If the input change in set up time, the output will be invalid.
     - If the input change in set up time, that means the combinational circuit between the flip-flop is too slow. You might have to split the circuit and insert another flip-flop in the middle.
 - Hold time
     - The time after rising edge of the clk that the input must not change
     - If the input change in hold time, the ouput will be invalid.
     - If the input change in hold time, that means the combinational circuit is too fast, you need to slow it down by adding ... 

the time that data arrive should be between clk+hold_time and clk+set_up_time

:::info
Hold time error typically will be slowed down by the routing delay.
:::