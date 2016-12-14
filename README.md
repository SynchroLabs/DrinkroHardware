#Introduction

This is a controller board with two L293D H-Bridge ICs used to run four DC
motors. In my application I used a 12VDC power supply and four 12VDC
peristaltic pumps for pumping drink ingredients.

The master branch of this repo may not be completely tested and ready to
produce. For a stable version, look at the release tags.

We are using this board in conjunction with a [Raspberry Pi 3 Model
B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) and iOS,
Android, Windows Phone and Windows [drink
software](https://github.com/SynchroLabs/Drynkro) built with the [Synchro
platform](https://synchro.io).

#Hooking Things Up

The motors are hooked up to `J11`-`J14`. Plug in a DC power supply to `J1`.

Note that each motor can draw up to 300mA, so make sure that your DC power
supply can handle it if you want to drive more than one motor at a time.

Connect `J10` to a Raspberry Pi / Arduino / whatever you want as a controller.
Provide `VCCIO`, this must match your controller GPIO voltage, and connect
`GND`. `MOTOR1_EN` etc. are the motor enable lines, and can be PWM controlled
for speed control, or hooked up to regular GPIOs. I have not done a lot of
testing with speed control, I just turn the motors completely on and off with a
regular GPIO. The motor control lines have a pulldown resistor -- if these are
not installed, then the motor may default to enabled, depending on the L293D
chip you use. I'm using the ST Micro version and this was the case for that
chip.

`J2`-`J9` are used for motor direction. Each header has a VCCIO and a GND pin.
`DIR1` and `DIR2` must be set to opposite values -- that is, set `J2`
(`MOTOR1_DIR1`) to jumper to `VCCIO`, then set `J3` (`MOTOR1_DIR2`) to jumper
to `GND`. See the L293D datasheet for more information about how this works
internally in the chip. If the motor is running the wrong direction (pumping
the wrong way in my case), then swap both jumpers. If you want, you can skip
the jumpers and drive the direction pins directly from your controller.
However, there are no pullups or pulldowns on the lines, so be careful about
enabling a motor with the direction pins floating. I use jumpers in my case as
I don't care to run the pumps in reverse.

#Other Stuff

This is a good writeup on version control and EAGLE

https://spin.atomicobject.com/2015/01/19/hardware-version-control/

Some design considerations surround the current on VCC. Each motor can draw up
to 600mA, so the total current on VCC can be up to 2.4A (all four motors
running). Using the calculator at http://www.4pcb.com/trace-width-calculator.html
you need to make sure the trace width is suitable. The minimum trace for 2.4A
on 1oz copper is ~40mil.
