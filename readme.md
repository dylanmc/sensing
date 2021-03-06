# sensing kits

Made for/with the [PNCA Sensing the Environment Project](http://pnca.edu/makethinkcode/news/c/sensing_the_environment).

This is a sound recording and reporting kit. Right now, sound is recorded to an onboard SD card. 
Stage 1 will send this info over Wifi to a Python server on a host computer.

## objectives
- record bird songs at night for as long as possible (1-2weeks)
- transmit bird songs to cloud server after recording is finished (during the day)
- connect to cloud server to download recorded data
- make a recording device that is cheap and easy to setup and maintain

## software

For the Rpi:
- Image of RPi_sensing (TODO: make and post image of pi with everything configured proper) 

For the computer:
- Python 2.*
- Virtualenv & virtualenvwrapper
- [pip](https://pip.pypa.io/en/stable/)

## software overview

- a python script takes care of sending files to ftp server on a schedule
- a built-in linux program called arecord takes care of recording data on a schedule
- a shell script takes care of recording intervals and generating Pi-specific (using MAC address) filenames
- witty pi software and hardware takes care of sleep/wake schedules

## hardware

You will need:
-[Raspberry Pi 3 model B]
-[Sabrent USB sound card adapter]
-[Sparkfun Sound Detector or Adafruit Amplifier]
-[Witty Pi 2 Cape for Rpi]
-[microSD card (8GB is fine)]
-[USB thumb drive (128GB)]
-[Waterproof enclosure ]
-[small waterproof gland (for microphone) PG7]
-[medium waterproof gland (for AC power) PG9]
-[Minimum 2.1A 5VDC power supply]
-[AC extension cord]
-[shielded microphone cable ]

Optional accessories :
-[HDMI cable],
-[HDMI monitor],
-[USB keyboard]
-[USB mouse]
- [Wireless dongle w/ removable 5dB antennae that works with Pi(optional) (enhancement for larger range)]
-[Hardware for standoffs]
-[acrylic sheets for mounting plate (enclosure)]

## hardware overview

An SFTP server installed on an Intel Nuc  will live at Dylan's place  

An SFTP client install on the Rpi lives in the field

## Installation of USB audio device and Arecord

On the raspberry pi, follow the setup on [raspberry pi audio setup](http://www.g7smy.co.uk/2013/08/recording-sound-on-the-raspberry-pi/) 

then test recording with:

arecord -f S16_LE --r=22000 -D plughw:1 --max-file-time 30 --duration=10 -vv ~/rectest11.wav
 
## configuration of pi

the witty pi software uses a script to control when to go to sleep and wake up found in 
/wittypi/schedules/

edit the etsyhost name to be unique:

1. sudo nano /etc/hosts


## configuration of arecord

duration is the maximum length of chunks in seconds

max file time is the ultimate length of recording in seconds

## using a virtual environment

On the host computer, in the project directory, run the following commands to set up your Python environment:

```
mkvirtualenv sensing
pip install -r requirements.txt
```

This should install `pyserial` locally in your `sensing` virtual environment.

run `brew install sox` to get SoX on your computer.


### virtualenvs

To work in your virtualenv, run the command `workon sensing`. To leave, run `deactivate`.

## project structure

- `/teensy` stores Teensy sketches for microcontroller based sensing module (legacy)
- `/RPi` will store "base station code"; i.e., the client with the microphone sensing unit that reports data back to server and a basic frontend to confirm that communication is working.
- `/raspberry_pi` will store "base station code"; i.e., the client with the microphone sensing unit that reports data back to server and a basic frontend to confirm that communication is working.
- `/docs` a place to store all documentation for this project 
- `/enclosure` a place to store all things enclosure related - design files for 3d printing and laser cutting 

## development
Slack
- Hackathon: Sensing the Environment
- Workspace URL: sensingtheenvironment.slack.com 

## building from source
- download latest version of NOOBs or Debian Jessie/Wheezy 
- update software 
- configure keyboard, locale, and timezone as US.
- clone this repo 
- run python script as a bash script on startup
- follow [raspberry pi audio setup](http://www.g7smy.co.uk/2013/08/recording-sound-on-the-raspberry-pi/) to make sure you can record with your setup



## references
- [microphone jack schematic](https://electronics.stackexchange.com/questions/307430/confusion-about-trrs-jack-and-mic-input)
- [microphone jack pic](https://cdn.instructables.com/ORIG/FHZ/YTV8/GAPUWXXX/FHZYTV8GAPUWXXX.jpg)
- [raspberry pi audio setup](http://www.g7smy.co.uk/2013/08/recording-sound-on-the-raspberry-pi/)

## credits
Nandini
Violet Pena
Trace Harris
Richard
Dylan Mcnamee
Chris Eykamp
Candace Hazelwood
Jesse Jenkins
Daniel Tiebel

## troublehsooting known bugs

- raspberry pi gives error : could not get clock with witty pi installed