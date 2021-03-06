---
title: Grove - Piezo Vibration Sensor
category: Sensor
bzurl: https://seeedstudio.com/Grove-Piezo-Vibration-Sensor-p-1411.html
oldwikiname: Grove_-_Piezo_Vibration_Sensor
prodimagename: Grove-Piezo_Vibration_Sensor-1.jpg
bzprodimageurl: http://statics3.seeedstudio.com/seeed/img/2016-06/VGKGp4ZlaglN4DMgnVAhUzUz.jpg
surveyurl: https://www.research.net/r/Grove-Piezo_Vibration_Sensor
sku: 101020031
tags: grove_analog, io_3v3, io_5v, plat_duino, plat_pi
---

![](https://raw.githubusercontent.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/master/img/Grove-Piezo_Vibration_Sensor-1.jpg)

![](https://raw.githubusercontent.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/master/img/Piezo_Vibration_Sensor_02.jpg)

Grove- Piezo Vibration Sensor is suitable for measurements of flexibility, vibration, impact and touch. The module is based on PZT film sensor LDT0-028. When the sensor moves back and forth, a certain voltage will be generated by the voltage comparator inside of it. A wide dynamic range (0.001Hz~1000MHz) guarantees an excellent measuring performance. And, you can adjust its sensitivity by adjusting the on-board potentiometer with a screw.

[![](https://raw.githubusercontent.com/SeeedDocument/common/master/Get_One_Now_Banner.png)](http://www.seeedstudio.com/Grove-Piezo-Vibration-Sensor-p-1411.html)

## Features
--------

-   Standard grove socket
-   Wide dynamic range：0.1Hz~180Hz
-   Adjustable sensitivity
-   High receptivity for strong impact

!!!Tip
    More details about Grove modules please refer to [Grove System](http://wiki.seeed.cc/Grove_System/)

## Platforms Supported
-------------------

## Applications
------------
-   Vibration Sensing in Washing Machine
-   Low Power Wakeup Switch
-   Low Cost Vibration Sensing
-   Car Alarms
-   Body Movement
-   Security Systems

## Getting Started
-----

### With [Arduino](/Arduino "Arduino")

#### Connection

Here we will show you how this Grove - Piezo Vibration works via a simple demo. First of all, we need to prepare the below stuffs:

| Seeeduino V4 | Grove - Piezo Vibration | Base Shield |
|--------------|----------------------|-----------------|
|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_1.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/raw/master/img/Piezo%20vibration%20sensor_s.jpg)|![enter image description here](https://raw.githubusercontent.com/SeeedDocument/Grove_Light_Sensor/master/images/gs_4.jpg)|
|[Get ONE Now](http://www.seeedstudio.com/Seeeduino-V4.2-p-2517.html)|[Get ONE Now](https://www.seeedstudio.com/Grove-Piezo-Vibration-Sensor-p-1411.html)|[Get ONE Now](https://www.seeedstudio.com/Base-Shield-V2-p-1378.html)|

The Grove - Piezo Vibration Sensor outputs a logic HIGH when vibration was detected. We can use any of Arduino pins to read the data. Here is an example of Piezo Vibration Sensor controlling LED. When the vibration was detected, this sensor outputs a logic high signal (the sensitivity can be changed by adjusting the potentiometer), an LED lights up.

<div class="admonition note">
<p class="admonition-title">Note</p>
It may output low level even though originally output high level when you increase the threshold voltage by clockwise adjusting the potentiometer.
</div>

- Connect the module to the **A0** of base shield using the 4-pin grove cable, we use **digital pin13 on board LED** as output.
- Plug the Grove - Basic Shield into Arduino.
- Connect Arduino to PC by using a USB cable.
![](https://github.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/raw/master/img/piezo%20vibration%20connection.jpg)

#### Software

- Copy and paste code below to a new Arduino sketch.

```
const int ledPin=13;
void setup() {
    Serial.begin(9600);
    pinMode(ledPin,OUTPUT);
}

void loop() {
    int sensorValue = analogRead(A0);
    Serial.println(sensorValue);
    delay(1000);
    if(sensorValue==1023)
    {
        digitalWrite(ledPin,HIGH);
    }
    else
    {
        digitalWrite(ledPin,LOW);
    }
}
```
- Touch the piezo sensor to make it vibrate, of course, any way to make it vibrate will work. The LED will be on when vibration is detected. We can also Open the serial monitor to see the sensor outputs.

  ![](https://raw.githubusercontent.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/master/img/Grove-Piezo_Vibration_Sensor.jpg)

- We can directly use a digital pin, take D5 of base shield as an example, and connect LED to Pin 13.

```
const int ledPin=13;
void setup() {
    Serial.begin(9600);
    pinMode(ledPin,OUTPUT);
}

void loop() {
    int sensorState = digitalRead(5);
    Serial.println(sensorState);
    delay(1000);
    if(sensorState == HIGH)
    {
        digitalWrite(ledPin,HIGH);
    }
    else
    {
        digitalWrite(ledPin,LOW);
    }
}
```

### With Raspberry Pi

#### Connection
First of all, we need to prepare the below stuffs:

| Raspberry pi | Grove - Piezo Vibration | GrovePi_Plus |
|--------------|-------------|-----------------|
|![enter image description here](https://github.com/SeeedDocument/Grove-Temperature_and_Humidity_Sensor_Pro/raw/master/img/pi.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/raw/master/img/Piezo%20vibration%20sensor_s.jpg)|![enter image description here](https://github.com/SeeedDocument/Grove-Temperature_and_Humidity_Sensor_Pro/raw/master/img/grovepi%2B.jpg)|
|[Get ONE Now](https://www.seeedstudio.com/Raspberry-Pi-3-Model-B-p-2625.html)|[Get ONE Now](https://www.seeedstudio.com/Grove-Piezo-Vibration-Sensor-p-1411.html)|[Get ONE Now](https://www.seeedstudio.com/GrovePi%2B-p-2241.html)|

- Follow [instruction](http://wiki.seeed.cc/GrovePi_Plus/) to configure the development environment.
- Plug the sensor to grovepi+ socket A0 by using a grove cable.

![](https://github.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/raw/master/img/grove%20connection.jpg)

#### Software

- Navigate to the demos' directory:

```
    cd yourpath/GrovePi/Software/Python/
```
-   To see the code
```
    nano grove_piezo_vibration_sensor.py   # "Ctrl+x" to exit #
```
```
    import time
    import grovepi

    # Connect the Grove Piezo Vibration Sensor to analog port A0
    # OUT,NC,VCC,GND
    piezo = 0

    grovepi.pinMode(piezo,"INPUT")

    while True:
        try:
            # When vibration is detected, the sensor outputs a logic high signal
            print grovepi.analogRead(piezo)
            time.sleep(.5)

        except IOError:
            print "Error"
```

- Run the demo.
```
    sudo python grove_piezo_vibration_sensor.py
```

## Resources
---------

- **[Eagle]** [Grove - Piezo Vibration Sensor Eagle File](https://raw.githubusercontent.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/master/res/Eagle.zip)
- **[PDF]** [Grove - Piezo Vibration Sensor Schematic PDF File](https://raw.githubusercontent.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/master/res/Gvove-Piezo_Vibration_Sensor.pdf)
- **[PDF]** [Grove - Piezo Vibration Sensor PCB PDF File](https://github.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/raw/master/res/Gvove%20-%20Piezo%20Vibration%20Sensor%20v1.1%20PCB.pdf)
- **[Datasheet]** [Piezo Vibration Sensor Datasheet](https://raw.githubusercontent.com/SeeedDocument/Grove-Piezo_Vibration_Sensor/master/res/Piezo_Vibration_Sensor.pdf)


<!-- This Markdown file was created from http://www.seeedstudio.com/wiki/Grove_-_Piezo_Vibration_Sensor -->
