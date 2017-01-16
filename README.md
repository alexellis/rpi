WiringPi-Go
============

> This library has been forked for experimental use / research by Alex Ellis. I'm looking to use this to port the Pimoroni Blinkt! library to Golang. If you'd like to help or are in a similar position (looking for a GPIO library for Golang) get in touch.

Golang wrapped version of Gordon's Arduino-like WiringPi for the Raspberry Pi

# Install Go

If you don't have Go on the Pi, download it from: https://golang.org/dl/ and pick the armv6l edition.

```
sudo tar -xvf go1.7.4.linux-armv6l.tar.gz -C /usr/local/
export GOPATH=$HOME/go
```

Create your first project under: `$HOME/go/src/github.com/youruser/yourrepo/`

# Installation

Install WiringPi

```
# sudo apt-get install -qy wiringpi
```

Then get the library:

```
go get github.com/alexellis/rpi
```

# GPIO numbering

wiringPi   | Name     | GPIO.BOARD    | GPIO.BCM
---------- | -------- | ------------  | --------
0          |GPIO 0    | 11            | 17 
1          |GPIO 1    | 12            | 18
2          |GPIO 2    | 13            | 21
3          |GPIO 3    | 15            | 22
4          |GPIO 4    | 16            | 23
5          |GPIO 5    | 18            | 24
6          |GPIO 6    | 22            | 25
7          |GPIO 7    | 7             | 4
8          |SDA       | 3             | 0
9          |SCL       | 5             | 1
10         |CE0       | 24            | 8
11         |CE1       | 26            | 7
12         |MOSI      | 19            | 10
13         |MOSO      | 21            | 9
14         |SCLK      | 23            | 11
15         |TXD       | 8             | 14
16         |RXD       | 10            | 15

more to read at: [http://hugozhu.myalert.info/2013/03/22/19-raspberry-pi-gpio-port-naming.html](http://hugozhu.myalert.info/2013/03/22/19-raspberry-pi-gpio-port-naming.html)

# Sample codes

## `lcd.go`
```go
package main

import (
    . "github.com/alexellis/rpi"
)

func main() {
    WiringPiSetup()

    //use default pin naming
    PinMode(PIN_GPIO_4, OUTPUT)
    DigitalWrite(PIN_GPIO_4, LOW)
    Delay(400)
    DigitalWrite(PIN_GPIO_4, HIGH)

    //use raspberry pi board pin numbering, similiar to RPi.GPIO.setmode(RPi.GPIO.BOARD)
    Delay(400)
    DigitalWrite(BoardToPin(16), LOW)
    Delay(400)
    DigitalWrite(BoardToPin(16), HIGH)

    //use raspberry pi bcm gpio numbering, similiar to RPi.GPIO.setmode(RPi.GPIO.BCM)
    Delay(400)
    DigitalWrite(GpioToPin(23), LOW)
    Delay(400)
    DigitalWrite(GpioToPin(23), HIGH)
}
```

## Run

```
export GOPATH=`pwd`
go install github.com/alexellis/rpi 
```
