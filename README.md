VarSpeedServo
===============

This Arduino library allows the use of up to 8 servos used with an Arduino. Since it uses interrupts, servos can run asynchronously. The libarary also permits the setting of the speed of a move, and a write() call to position can wait and only return when the move is finished.

This code is an adaptation of the standard Arduino Servo library, which was first adapted by Korman and posted on the [Arduino forum](http://forum.arduino.cc/index.php?topic=61586.0) to add the speed capability. Philip van Allen updated it for Arduino 1.0 + and added the ability to to wait for the move to complete.

* Supports up to 8 servos
* Allows simultaneous, asynchronous movement of all servos
* Speed of the move can be set
* A servo write() function to set a new position can wait for completion before returning
* Allows the use of sequences of servo positions, where the servo can go at a specified speed to each position in order

Sample Code
----------------------------

	#include <VarSpeedServo.h> 
	 
	VarSpeedServo myservo;    // create servo object to control a servo 
	 
	void setup() {
	  myservo.attach(9);  // attaches the servo on pin 9 to the servo object 
	} 
	 
	void loop() {
	  myservo.write(180, 30, true);        // move to 180 degrees, use a speed of 30, wait until move is complete
	  myservo.write(0, 30, true);        // move to 0 degrees, use a speed of 30, wait until move is complete
	}

Additional examples are included in the distribution and are available in the Arduino Examples section.

Class methods
================

A servo is activated by creating an instance of the Servo class passing the desired pin to the attach() method. The servos are pulsed in the background using the value most recently written using the write() method
 
VarSpeedServo - Class for manipulating servo motors connected to Arduino pins. Methods:

	attach(pin )  - Attaches a servo motor to an i/o pin.
	attach(pin, min, max  ) - Attaches to a pin setting min and max values in microseconds
	default min is 544, max is 2400  

	write(value)     - Sets the servo angle of value in degrees.  (invalid angle that is valid as pulse in microseconds is treated as microseconds)
	write(value, speed) - speed varies the speed of the move to new position 0=full speed, 1-255 slower to faster
	write(value, speed, wait) - wait is a boolean that, if true, causes the function call to block until move is complete

	writeMicroseconds() - Sets the servo pulse width in microseconds 
	read()      - Gets the last written servo pulse width as an angle between 0 and 180. 
	readMicroseconds()   - Gets the last written servo pulse width in microseconds. (was read_us() in first release)
	attached()  - Returns true if there is a servo attached. 
	detach()    - Stops an attached servos from pulsing its i/o pin. 

	slowmove(value, speed)  - The same as write(value, speed), retained for compatibility with Korman's version

	sequenceInit(sequenceIndex, arrayOfPositionSpeedPairs, numberOfPairs); // set up a sequence for a specific index
   	sequencePlay(sequenceIndex, loop); // play a sequence starting at position 0 at first move
   	sequencePlay(sequenceIndex, loop, startPos); // play a sequence starting at a specified position
   	sequenceStop(); // stop current sequence at current position

Installation
=============

* Download the .zip file from the releases section of GitHub
* In Arduino, select SKETCH>IMPORT LIBRARY...>ADD LIBRARY... and find the .zip file
* This will install the library in your My Documents (Windows) or Documents (Mac) folder under Arduino/libraries
* You can also unzip the file, and install it in the above libraries folder manually
* See [arduino.cc/en/Guide/Libraries](http://arduino.cc/en/Guide/Libraries) for more info on libraries