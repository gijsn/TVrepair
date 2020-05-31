# TVrepair
> Repair of a Philips 55PFL8007 55" ambilight TV showing 2 flashes with 3 seconds pause (works for most Philips TV's 2013 era)

Hi all, 
After an evening of wathcing TV suddenly the TV stopped working showing short flashes and later, after a reboot, nothing at all.
The next day, I spend a long afternoon troubleshooting and fixing the TV using the repair manual you can find in this repo. I got it from https://www.manualslib.com/manual/1072511/Philips-40pfl8008k-12.html#manual, which might be better as some paged in the PDF are misaligned and fall off the page edge

First step, as always, look for any obvious burnt spots on the boards, and then, thou shall measure voltages. Removing the back cover, you find two flatflexes connected to the back cover supplying the ambilight. The flatflex cables can stay connected as long as you have enough space to fit both the TV and cover in a single area. I used the kitchen table to make it work. This is what we found:

1. None of the boards inside showed any burnt areas or bulged capacitors of any sort. Also measuring the caps that allowed themselves to be measured came up nothing.
2. There are two main boards visible (your milage may vary), one 'SSB' and one power supply board, this also integrates the LED backlight driver, where I suspected the fault to be, as the voltage read 55V instead of the 82.5V the silkscreen read. There are some control lines coming from the SSB board to probably adjust the voltage there, so there is no definitive solution to what could be at fault. The manual supplies no information about the power supply module and takes it as a 'black box, replace if broken' element. 
3. Next, I figured after a while the 12V supply to the SSB board would shutdown after a while, even though the polyfuses on the board (1UA0 1UA1 and 1UP1) checked out fine. 
4. Following the flowcharts in the manual showing the boot procedure, It was soon figured that the processor was not falling through 'MIPS boot' section somewhere. A connection to the UART port was made (duh, should have done that first). This thing is broken out as a 3.5mm connector on the backside of the TV. The service manual can help with the pinout connection but the TX is at the tip of the connector, and GND at the back. Use a terminal application at baud 115200, 8,1,N
5. Read the output of the boot process and google it! This is where I ended up very soon: https://alpengeist-tvrepair.blogspot.com/2018/12/philips-55pfl6158-2-blinks-qfu-12-cpu.html (thanks!!), always useful if multiple people have the same problem! Reading the UART of such a device was a first for me! Really interesting if it actually produces something.
6. From there on, I followed the steps mentioned in that blogpost.
I attached some imagery to help you guide along the process, the TV is now working again!

TL;DR
The final recipe came out to be:
5 minutes, 210 degrees C for the green SSB board.
Cover all but the main processor (the one with the heatsink) with aluminium foil, put it in a preheated oven for 5 minutes. Then, let it cool down passively in the oven until cool enough to touch. Success rate might vary

