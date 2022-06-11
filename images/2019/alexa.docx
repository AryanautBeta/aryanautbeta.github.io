import subprocess
import os
import tempfile
import shlex
import time
import RPi.GPIO as GPIO
import time
from neopixel import *
import argparse
 

#Led config
LED_COUNT      = 16      # Number of LED pixels.
#LED_PIN        = 18       # GPIO pin connected to the pixels (18 uses PWM!).
LED_PIN        = 10      # GPIO pin connected to the pixels (10 uses SPI /dev/spidev0.0).
LED_FREQ_HZ    = 800000  # LED signal frequency in hertz (usually 800khz)
LED_DMA        = 10      # DMA channel to use for generating signal (try 10)
LED_BRIGHTNESS = 255     # Set to 0 for darkest and 255 for brightest
LED_INVERT     = False   # True to invert the signal (when using NPN transistor level shift)
LED_CHANNEL    = 0       # set to '1' for GPIOs 13, 19, 41, 45 or 53


#Comment the line below if you want to create your own indicator pattern
#from alexaindicator import assistantindicator

#thinking and listening
strip = Adafruit_NeoPixel(LED_COUNT, LED_PIN, LED_FREQ_HZ, LED_DMA, LED_INVERT, LED_BRIGHTNESS, LED_CHANNEL)
strip.begin()
def listen(strip, color, wait_ms = 50):
    for i in range(strip.numPixels()):
        strip.setPixelColor(i, color)
        strip.show()
        strip.setPixelColor(i-1, Color(0,0,50))
        time.sleep(wait_ms/1000.0)

def speak(strip, r, g, b):
    nFade = 50
    c = 255
    for i in range(nFade):
        colOn = Color(0, 0, int((i*c)/float(nFade)))
        for j in range(strip.numPixels()):  
            strip.setPixelColor(j, colOn)
            strip.show()
    for v in range(nFade):
        colOff = Color(0, 0, int(((255-v)*c)/float(nFade)))
        for a in range(strip.numPixels()):    
            strip.setPixelColor(a, colOff)
            strip.show() 

def authorize(strip, color):
    for i in range(strip.numPixels()):
        strip.setPixelColor(i, Color(0,0,255))
        strip.show()
        time.sleep(10/1000.0)
    for j in range(strip.numPixels()):
        strip.setPixelColor(j, Color(0,0,0))
        strip.show()
        time.sleep(10/1000.0)

def clear(strip):
    for x in range(strip.numPixels()):
        strip.setPixelColor(x, Color(0,0,0))
        strip.show()


ROOT_PATH = os.path.realpath(os.path.join(__file__, '..', '..'))
USER_PATH = os.path.realpath(os.path.join(__file__, '..', '..','..'))


def run_command(command):
    process = subprocess.Popen(shlex.split(command), stdout=subprocess.PIPE)
    while True:
        time.sleep(.1)
        output = process.stdout.readline()
        if output == '' and process.poll() is not None:
            break
        if output:
            print(output.strip())
            if "authorized" in str(output.strip()).lower():
                #Change the path to your desired audio file for the startup tone
                subprocess.Popen(["aplay", "{}/home/pi/sounds/med_ui_wakesound.wav".format(USER_PATH)], stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
                authorize(strip, Color(0, 0, 0))
                #Comment the line below if you want to create your own indicator pattern
                #assistantindicator('off')
            if "listening..." in str(output.strip().lower()):
                #Change the path to your desired audio file for the trigger alert tone
                subprocess.Popen(["aplay", "{}/home/pi/sounds/med_ui_wakesound.wav".format(USER_PATH)], stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
                listen(strip, Color(0, 0, 255))
                listen(strip, Color(0, 0, 255))
                #Comment the line below if you want to create your own indicator pattern
                #assistantindicator('listening')
            if "speaking..." in str(output.strip()).lower():
                #Comment the line below if you want to create your own indicator pattern
                #assistantindicator('speaking')
                speak(strip, 0, 0, 255)
		print('speaking\n')
            if "idle!" in str(output.strip().lower()) or "SPEAKING,to=IDLE" in str(output.strip()):
		#Comment the line below if you want to create your own indicator pattern
                clear(strip)
                #assistantindicator('off')
		print('off\n')
		
    rc = process.poll()
    return rc

#Change the path to your startsample file
run_command("sudo bash {}/pi/sdk-folder/sdk-source/avs-device-sdk/tools/Install/startsample.sh".format(USER_PATH))
