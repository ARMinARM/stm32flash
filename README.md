stm32flash
==========

**[2015-12] upstream moved to: http://sourceforge.net/p/stm32flash/code/ci/master/tree/ You'll probably want to use that, as this version is outdated.**

Open source flash program for the STM32 ARM processors using the ST serial bootloader over UART or I2C

stm32flash 0.4 was released 2014-10-04 and is available at https://releases.stm32flash.googlecode.com/git/stm32flash-0.4.tar.gz

The 0.4 version is the work of Antonio Borneo and includes support for programming over I2C. See the included I2C.txt for more information. The code has been refactored to make it easier to add other transports.

Features
--------

- UART and I2C transports supported
- device identification
- write to flash/ram
- read from flash/ram
- auto-detect Intel HEX or raw binary input format with option to force binary
- flash from binary file
- save flash to binary file
- verify & retry up to N times on failed writes
- start execution at specified address
- software reset the device when finished if -R is specified
- resume already initialized connection (for when reset fails, UART only)
- GPIO signalling to enter bootloader mode (hardware dependent)

Usage
-----

See the included manual page for up-to-date, complete usage instructions.

	Usage: ./stm32flash [-bvngfhc] [-[rw] filename] /dev/ttyS0
			-b rate         Baud rate (default 57600)
			-r filename     Read flash to file
			-w filename     Write flash to file
			-u              Disable the flash write-protection
			-e n            Only erase n pages before writing the flash
			-v              Verify writes
			-n count        Retry failed writes up to count times (default 10)
			-g address      Start execution at specified address (0 = flash start)
			-s start_page   Flash at specified page (0 = flash start)
			-f              Force binary parser
			-h              Show this help
			-c              Resume the connection (don't send initial INIT)
							*Baud rate must be kept the same as the first init*
							This is useful if the reset fails

Examples
--------

Get device information:

	./stm32flash /dev/ttyS0

Write with verify and then start execution:

	./stm32flash -w filename -v -g 0x0 /dev/ttyS0

Read flash to file:

	./stm32flash -r filename /dev/ttyS0

Start execution:

	./stm32flash -g 0x0 /dev/ttyS0

Authors
-------

stm32flash was originally written by Geoffrey McRae and is since 2012 maintained by Tormod Volden. See the git log for the many other contributors.
