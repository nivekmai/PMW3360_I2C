# PMW3360 I2C Interface

Implementation of [SunjunKim's PMW3360 library](https://github.com/SunjunKim/PMW3360) to send the data over I2C (acting as an I2C target sending mouse data to the controller).

The code is designed for Arduino style microcontrollers and tested on a seeeduino xiao.

# PMW3360 class
Notice: The PMW3360 class is from https://github.com/SunjunKim/PMW3360, which is based on https://github.com/mrjohnk/PMW3360DM-T2QU

* void begin(unsigned int ss_pin, unsigned int CPI = 800)
  * Initialize the sensor. ss_pin is Slave Select pin on the module. Optionally CPI value can be set.
* void setCPI(unsigned int newCPI); / unsigned int getCPI();
  * Set/get CPI (Count per Inch).
* PMW3360_DATA readBurst();
  * Read sensor motion data using burst mode operation.
  * PMW3360_DATA is a struct that contains various information about a motion.
	  - PMW3360_DATA.isMotion      : bool, True if a motion is detected. 
	  - PMW3360_DATA.isOnSurface   : bool, True when a chip is on a surface 
	  - PMW3360_DATA.dx, data.dy   : integer, displacement on x/y directions.
	  - PMW3360_DATA.SQUAL         : byte, Surface Quality register, max 0x80
	                               * Number of features on the surface = SQUAL * 8
	  - PMW3360_DATA.rawDataSum    : byte, It reports the upper byte of an 18‐bit counter 
	                               which sums all 1296 raw data in the current frame;
	                               * Avg value = Raw_Data_Sum * 1024 / 1296
	  - PMW3360_DATA.maxRawData    : byte, Max/Min raw data value in current frame, max=127
	    PMW3360_DATA.minRawData
	  - PMW3360_DATA.shutter       : unsigned int, shutter is adjusted to keep the average
	                               raw data values within normal operating ranges.
* byte readReg(byte reg_addr);
  * Read register value from the module.
* void writeReg(byte reg_addr, byte data);
  * Write register value to the module.
 
# License

Copyright (c) Kevin Christensen. All right reserved.

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA

# Update log
* v1.0.0
  * Initial release
