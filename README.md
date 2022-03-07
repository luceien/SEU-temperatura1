# SEU-temperatura1

In the subject '*Sistemas empotrados y ubicos*' at the **Escuela Técnica Superior de Ingeniería Informática** (UP Valencia), we have worked on an *embedded system* to have the temperature and create states according to its level.

## Composition

Our system is made out of 4 LEDs, one buzzer, several resistances and capacities, switches, Negative Temperature Coefficient Thermistor (NTC) and also an **ESP8266**. It was all organized as shown below with a computer connected to D2 to display the outputs.
 
 
![alt text](https://github.com/luceien/SEU-temperatura1/blob/main/Images/schema.jpg)
 
  
This ESP8266 is crucial in order to control all the components and make requests via a wifi network. Here is its [pinout](https://components101.com/development-boards/nodemcu-esp8266-pinout-features-and-datasheet "ESP8266 Pinout") 
 
  
![alt text](https://github.com/luceien/SEU-temperatura1/blob/main/Images/ESP8266.jpg)
 

## How it works

The goal of the project was to retrieve and display real-time temperature information and create the following situations :
- If the temperature is **below 23°C**, all the *lights are off*.
- From 23°C, a **light will turn on every 3°C** until 32°C where they are all on.
- An emergency **buzzer rings at 34°C**.
 
 
To develop the project, I decided to split it in **three threads**. One is used to *display the data* we have collected (temperature and time) by reading the buffer, another is used to handle everything related to the temperature which means **reading the temperature on the NTC** and **lighting the right LEDs** or activating the buzzer depending on the temperature.
The last thread is used to handle everything related to the **time** which means **connecting to the wifi** to collect and clean the json file so that I can display it.


We use *ESP8266* to connect to the wifi and go through [**worldclockapi.com**](worldclockapi.com) to obtain time in JSON format and, on the other hand, we use a NTC to obtain the temperature.

The file *utility.c* allows to get information and display them in the terminal : 
 
![alt text](https://github.com/luceien/SEU-temperatura1/blob/main/Images/temperature.jpg)
 
 
Finally, I send the temperature value in the **buffer** with *temperature_buffer_write* to update *lights_list* and *buzzer*. Thus, the function *set_lights_and_buzzer* updates states of the lights and buzzer to match the requirements.
