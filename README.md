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

###Comm.h
this header file provide access and functionality to the Serial port on the arduino.

***please note:** the original designers of the Kaimana board used digital pins 0 (RX) and 1 (TX) for button IO. *

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