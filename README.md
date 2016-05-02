This is a good writeup on version control and EAGLE

https://spin.atomicobject.com/2015/01/19/hardware-version-control/

Some design considerations surround the current on VCC. Each motor can draw up
to 600mA, so the total current on VCC can be up to 2.4A (all four motors
running). Using the calculator at http://www.4pcb.com/trace-width-calculator.html
you need to make sure the trace width is suitable. The minimum trace for 2.4A
on 1oz copper is ~40mil.
