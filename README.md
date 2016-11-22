# Kaimana Redux

this is a public repo for a **basic version** of a mash up between the slimmed down **[moledcule](http://moledcule.club)** version of original Kaimana code

the intent behind this code is to normalize and introduce efficiencies to the existing Kaimana code base

in the **examples folder** you will find a few sketches *(currently there is only 'basic')*

-----

##basic example
files:
* basic.ino *(main program)*
* Comm.h *(all comm port utilities)*
* Pins.h *(input output functionality)*
* Structures.h *(structs definitions for program)*
* Utils.h *(transformation utilities)*

-----

###basic.ino
how are pins mapped to the Kainana device
```
                                      +-----+
         +----[PWR]-------------------| USB |--+
         |                            +-----+  |
         |         GND/RST2  [ ][ ]            |
         |       MOSI2/SCK2  [ ][ ]  A5/SCL[ ] |
         |          5V/MISO2 [ ][ ]  A4/SDA[ ] |
         |                             AREF[ ] |
         |                              GND[ ] |
         | [ ]N/C                    SCK/13[ ] |
         | [ ]IOREF                 MISO/12[ ] | Kick 3
         | [ ]RST                   MOSI/11[ ]~| Down
         | [ ]3V3    +---+               10[ ]~| Start
         | [ ]5v    -|   |-               9[ ]~| Select
         | [ ]GND   -| A |-               8[ ] | Home
         | [ ]GND   -| 3 |-                    |
         | [ ]Vin   -| 2 |-               7[ ] |
         |          -| U |-               6[ ]~| Kick 4
      Up | [ ]A0    -| 4 |-               5[ ]~|
    Left | [ ]A1    -|   |-               4[ ] | Kick 1
   Right | [ ]A2     +---+           INT1/3[ ]~| Punch 1
  Kick 2 | [ ]A3                     INT0/2[ ] | Punch 2
         | [ ]A4/SDA  RST SCK MISO     TX>1[ ] | Punch 4
    Data | [ ]A5/SCL  [ ] [ ] [ ]      RX<0[ ] | Punch 3
         |            [ ] [ ] [ ]              |
         |  UNO_R3    GND MOSI 5V  ____________/
         \_______________________/

```
this file is pretty damn clean and easy to read, that was the whole intent

-----

###Comm.h

this header file provide access and functionality to the Serial port on the arduino.

*****please note:** *the original designers of the Kaimana board used digital pins 0 (RX) and 1 (TX) for button IO.****

####startComm
```
/*
** @method startComm
** @desc start serial port if DEBUG is defined
*/
startComm()
```

####listenComm
```
/*
** @method listenComm
** @desc listen to serial port if DEBUG is defined
*/
listenComm()
```

####printComm
```
/*
** @method printComm
** @param str (String)
** @desc print string to serial port if DEBUG is defined
*/
printComm(str)
```
-----

###Pins.h
this file contains the assignement of the IO struct to specific pins, their input, state, type, and last toggled timestamp

and example of the struct is as such

```
// definition
typedef struct {
	uint8_t pin;			// the pin for the input button
	uint8_t mode;			// INPUT | OUTPUT
	uint8_t state			// HIGH | LOW 
	String type;			// "a" | "d"
	unsigned long changed;	// last changed timestamp
} IO;	

// declaration example
IO FIRST_PUNCH = {1, INPUT, HIGH, "d", 0};
```

####printPins
```
/*
** @method printPins
** @desc create string buffer and dump to serial
*/
printPins
```

###setPins
```
/*
** @method setPins
** @desc itterate through structs and invoke setPins
*/
setPins
```

###getPins
```
/*
** @method getPins
** @desc itterate through structs and set appropriate structs
*/
getPins
```

-----

##Structure.h
nothing really exciting here, simply a place for all of the programs structs to live

-----
##Utils.h

###getBin
convert an interger into a binary string
```
/*
** @method getBin
** @param number (int)
** @return result {String} 
** @desc converts the decimal param to binary string
*/
String getBin(int number)
```

###getLong
convert an interger array into a long
```
/*
** @method getLong
** @desc convert rgb values to long int
** @param r {int} red value
** @param g {int} red value
** @param b {int} red value
** @return {long}
*/
long getLong(char r, char g, char b)
```

###getLong
convert an hexadecimal into a long
```
/*
** @method getLong
** @desc convert hex values to long
** @param color {hex} hex value represantation of color
** @return {long}
*/
long getLong(String color)
```

###getRGB
convert long into rgb array
```
/*
** @method getRGB
** @desc convert long values to rgb array
** @param color {long} long value represantation of color
** @return {int*}
*/
int* getRGB(unsigned long color)
```

###getRGB
convert long into the passed struct pointer
```
/*
** @method getRGB
** @desc convert long values to rgb array
** @param color {long} long value represantation of color
** @return {int*}
*/
RGB getRGB(RGB& rgb, unsigned long color)
```

###getHEX
convert long into hexadecimal
```
/*
** @method getHEX
** @desc convert long values to rgb array
** @param color {long} long value represantation of color
** @return {String}
*/
String getHEX(unsigned long color)
```

###getHEX
convert int array into hexadecimal
```
/*
** @method getHEX
** @desc convert long values to rgb array
** @param color {long} long value represantation of color
** @return {String}
*/
String getHEX(int* rgb)
```

with the Utils.h you can do crazy stuff like this

```
// you like purple
#define purple_hex "ffff00"

// you want to conver the above hex into an RGB struct
RGB purple_struct;

// you can nest utilities
getGRB(purple_struct, getLong(purple_hex))

// purple.r is now 255
// purple.g is now 0
// purple.b is now 255

```

***<u>have fun, play safe</u>***
