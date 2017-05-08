---
layout: post
---

  I have spent way too much time trying to program an attiny25/45/85 using an arduino as the ISP, both with Arduino 1.0 and avrdude on OSX Lion.
  I finally got an Arduino Nano v2.3 acting as an ISP for the attiny25 with avrdude on OSX Lion.
  Here is what I learned.

  TL;DR for those who just want to party
  --------------------------------------

    1. Install Arduino 1.0
    2. Wire up your board
    3. Open ArduinoISP, and change `Serial.begin(19200)` to `Serial.begin(9600)`
    4. Upload sketch to the arduino, make sure the heartbeat led on pin 9 is pulsing
    5. Put a 110->220 Ohm resistor between +5v and reset
    6. `cd /Applications/Arduino.app/Contents/Resources/Java/hardware/tools/avr/bin`
    7. `./avrdude -c stk500v1 -p attiny25 -P /dev/tty.usbserial-* -C ../etc/avrdude.conf -b 9600`

  Why all this work?
  ------------------
  The baudrate workaround is needed because the serial buffer size was halved between Arduino 023 to 1.0.
  It is already in the trunk version of ArduinoISP.

  The resistor is required to disable auto-reset on the arduino. If you are using a different board, make
  sure to learn how to disable auto-reset safely on that particular board. Also make sure to re-enable
  auto-reset when you want to put different firmware on the arduino.

  Can it be improved?
  -------------------
  If you have [homebrew][] installed, you can use [homebrew-alt][] to install a newer version of avrdude,
  which supports 'arduino' as a programmer, making the command:

  `avrdude -c arduino -b 9600 -p attiny25 -P /dev/tty.usbserial-*`

  This can be simplified further by telling avrdude to remember 9600 baud for arduino programming. Just add
  add `baudrate = 9600;` underneath `type = arduino;` in `/usr/local/etc/avrdude.conf`. Now its just:

  `avrdude -c arduino -p attiny25 -P /dev/tty.usbserial-*`

  Hopefully avrdude.conf will be updated to 9600 baud for the arduino programmer, as that seems to be
  the official fix.

  It would be even better if the libraries were updated so that 19200 baud would work with ArduinoISP.

  What about ATTiny support in the Arduino IDE?
  ---------------------------------------------
  There is an unofficial project that adds attiny entries to the Arduino IDE.

  To get this working, make sure to change the 19200 in `$ARDUINO_DIR/hardware/arduino/programmers.txt` to 9600.

  I will probably submit a patch to do this for you :)
