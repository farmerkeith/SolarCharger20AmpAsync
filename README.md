# Solar-charger-async version
MPPT Solar charger using an asynchronous DC-DC converter made from High-side P-channel MOSFETs and low side power diodes.
 
An Atmega328P is used for control including generating the pwm for the async converter.

It also has a supplementary input from mains supply controlled from the Nano, and a controlled Load output.

# Peripherals
Battery temperature is monitored with a DS18B20 sensor and used to adjust battery set points.

Operational data logging is provided by a micro SD card, with time stamps from a Tiny RTC module using a DS1307 IC. 

An LCD character display provides status information. A push button turns on the backlight of the LCD, saving power when the LCD is not required to be on. 

# Schematic
The schematic circuit diagram has been prepared using KiCad. 

12 May 2018. Added reset button. Added USB B-connector (for programming).
 Included spreadsheet analysis and system description document.

