# Embedded Systems Project
Interfacing DHT11 Temperature & Humidity Sensor with STM32F103C8
DHT11 is a Temperature and humidity sensor which as the name implies is used to measure the atmospheric temperature and humidity in a particular environment or in a confined closed space. The sensor is commonly used in monitoring environmental parameters in many applications like Agriculture, Food Industries, Hospitals, Automobile, Weather Stations etc.

The sensor could measure the temperature from 0°C to 50°C with an accuracy of 1°C. It is commonly used in controlled environments such as Heat ventilation systems, temperature chambers etc to monitor temperature and take corrective measures. The measuring range of humidity is from 20% to 90% with an accuracy of 1%. Humidity indicates the amount of water vapor present in the air. The value of humidity has to be kept within a controlled range in many scenarios like in manufacturing and storing of tea powders the correct humidity must be maintained in the room or the tea will lose its taste and smell. The level of humidity in living rooms should also be maintained within a comfortable range. The ideal value of humidity for maximum comfort is between 50% to 65%.

Today in this tutorial we will learn how to interface the popular DHT11 Temperature and Humidity sensor with STM32 microcontroller. We have already learnt the basics of STM32 board and how to use it Arduino IDE. For those who are new, the STM32 a.k.a BluePill development board, consists of the STM32F103C8T6 microcontroller from ST Microelectronics. It is a 32-bit ARM Cortex M3 controller with high clock frequency suitable for high speed and power constraint application.



# DHT11 Temperature & Humidity Sensor
Before proceeding with the interface procedure lets learn few things about the DHT11 sensor. As discussed earlier, the DHT11 sensor is used to measure Temperature and humidity. The sensor comes with a dedicated in-built NTC to measure temperature. It has an 8-bit microcontroller on-board to output the values of temperature and humidity as serial data through one-wire protocol. Meaning, the sensor has only one data pin through which both the temperature and humidity values can be read, thus saving pins on the microcontroller side. The sensor is also factory calibrated and hence easy to interface with other microcontrollers.

DHT11 Specifications:

Operating Voltage: 3.5V to 5.5V
Operating current: 0.3mA (measuring) 60uA (standby)
Output: Serial data
Temperature Range: 0°C to 50°C
Humidity Range: 20% to 90%
Resolution: Temperature and Humidity both are 16-bit
Accuracy: ±1°C and ±1%
![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/e5a928af-ec8a-47e6-8679-6e1da753a09f)


# Components Required
1. STM32F103C8
2. DHT11 Temperature & Humidity Sensor
3. 16x2 LCD Display
4. IIC/I2C Serial Interface Adapter Module
5. Breadboard
6. Connecting Wires


# Circuit Diagram
![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/33dfc2ab-bdf4-43ed-ab0b-766008a262d7)



As you can see, we have used an I2C interface module to connect the LCD module to STM32. This makes the connections simple and further reduces the number of pins used on the controller side. 

If you have an interface module, then the circuit Connections between I2C Serial Interface Module (Fixed with 16X2 LCD Display) & STM32F103C8 is tabulated below:
![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/47e4adf9-ce79-4566-ac10-3cd93f51127e)


Similarly the circuit Connections between STM32F103C8 and DHT11 Sensor is tabulated below.
![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/460ff4a0-3fd9-4e71-818c-1bfa34e5948c)

Once the connections are done my hardware looks something like this below.

![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/6d26c346-386b-49e6-9edc-440d974dfacc)

The entire set-up is powered by the USB port of STM32 from my laptop. Now that our hardware is ready, lets get into the coding part.


# Preparing the Arduino IDE for STM32F103C8
We have to write a program to read the temperature and humidity value from the DHT11 senor and display it on the LCD module. Here the LCD display is connected through I2C adapter, hence we have first find the I2C address of this adapter to communicate with LCD.

Interfacing I2C Serial LCD Interface Adapter Module with STM32F103C8:

From circuit diagram we can notice that the STM32F103C8 I2C pins PB6 and PB7 are connected with the SCL and SDA pins of I2C Serial Interface Module. To find the address of the I2C Serial Interface module we have to scan for available addresses.

Scanning the Address of the I2C Serial Interface Module:

Follow the below steps to find the I2C address of your LCD I2C interface module.

1. First check the STM32 package for Arduino IDE is installed. If not follow the link Programming your STM32 in ARDUINO IDE.

2. While installing packages for programming STM32 using Arduino IDE by above link the wire library is installed in default.

3.Program for scanning the I2C device connected is present in the examples (In Arduino IDE: Files->Examples->Wire->I2C scanner wire). Before that select the board in Tools->Board->Generic STM32F103C8 Series as shown below. 

Programming for DHT11 Sensor with STM32F103C

4. After then upload the code to the STM32F103C8 and the open serial monitor.

Interfacing Output of DHT11 Sensor with STM32F103C8

Now note the I2C address of the I2C 16x2 LCD display as (0x27).

Installing Library for I2C 16x2 Display Module and DHT11 Sensor: 

Now that we know the I2C address we need to download a library for communicating to the LCD display through I2C. The I2C LCD display library can be downloaded from this link. After downloading the zip file install I2C LCD library in the Arduino IDE by sketch->import library.This library can also be used with Arduino boards for communicating with I2C LCD display modules.

Similarly in order to read the serial data from DHT11 sensor we will use the DHT11 library. Download the library as a ZIP file using the link provided and after downloading, install DHT library in the Arduino IDE by using sketch->import library. Again the same library can also be used with Arduino boards.

![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/875219ff-2d9c-48f7-a34c-017715cd76f2)

If your displays shows nothing you can check adjusting the contrast potentiometer at the back of the I2C module. I tried varying my room temperature using an Air conditioner and found the sensor value to also vary accordingly. The AC also has an option to measure room temperature and as you can see in below image my remote displays the room temperature to be 27°C and our sensors also displays 27.3°C on the LCD which is pretty much close.

![image](https://github.com/jaswanthgodavathi/embedded_systems/assets/92353360/b0f71bc1-1cc7-44c4-970d-fd90df522d7d)

