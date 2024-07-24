# CD74HC4067_multiplexer_notes

My notes on using multiple CD74HC4067 multiplexers (or MUX) with the arduino platform to allow 32 channels and more

I'm making these notes as I found it hard to get information about this on the internet, and got quite stuck for a while. 

Firstly make sure that you can use a single CD74HC4067 board and that all is working. 

![image](https://github.com/user-attachments/assets/43199f48-702f-45a5-ab0c-1d0a8da0e671)

I'm using one of these cheap boards. 

GND   -> GND
VCC   -> VCC - so the working voltage of your board. Will be 3v normally, sometimes 5v
EN    -> any output pin on your microcontroller. If this is pulled LOW the board is on, if pulled HIGH then the board is off. If only usinfg one board you can conect this to GND
S0    -> any output pin  |
S1    -> any output pin  |  these pins are how you select which channel on the MUX you are accessing. I think it's a very simple binary system as 1111 is 15
S2    -> any output pin  |
S4    -> any output pin  |
SIG   -> any pin relevent to what you want to achieve. So an analogue pin for analogue readings. A digital pin for digital. My experience is that I have had to use a resistor for pull up or pull down to get consistent results and that the internal pullup/pulldown is not powerful enough. 

I am using this library https://github.com/waspinator/CD74HC4067

The way it works is that you select the pin on the MUX using the library or pins SO, S1, S2, S3 and then interact with the SIG pin to get what you need done. Repeat on the next channel etc. 

For multiple boards you need to have a different EN pin for each one so you can switch which board you are reading from and a seperate SIG pin as well. The SIG will need to have an extenal resistor for pull or pull down otherwise my experience is that I have had some weird readings. 

Lastly and a little tangentilly a reminder that not all pins on an ESP32 are multi use. Some are input only and have no built in pullup anyway. 

That's it really
