# Controller

The Motion Controller is based on the 5A-75B wich is a cheap LED Driver Board.

### Why?

The Board has two 1 GBit/s NICs, has 16 HUB75-connectors, with each 6 individual pins (96 total). Besides these pins, there are 8 shared pins. This makes the total number of usable pins 104.

### Idea

The idea is to desolder the 74HC245T Chips (levelshifters) and directly attach the FPGA to the connector to use some IOs as Input Pins. 


https://zeromips.org/posts/2022-05-29-5a-75b/
