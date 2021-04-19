# SIT210-Task5.2C-RPiGUI

from tkinter import *
import tkinter.font
from gpiozero import LED
import RPi.GPIO

RPi.GPIO.setmode(RPi.GPIO.BCM)

Redled = LED(14)
Greenled = LED(18)
Blueled = LED(12)

win = Tk()
win.title("Turn on led")
myFont = tkinter.font.Font(family = 'Helvetica', size = 12, weight = "bold")

def redLedToggle():
    if Redled.is_lit:
        Redled.off()
        ledRedButton["text"] = "Turn red LED on"
    else:
        Redled.on()
        Greenled.off()
        ledRedButton["text"] = "Turn red LED off"
        
def greenLedToggle():
    if Greenled.is_lit:
        Greenled.off()
        ledGreenButton["text"] = "Turn green LED on"
    else:
        Greenled.on()
        Redled.off()
        ledGreenButton["text"] = "Turn green LED off"
        
def blueLedToggle():
    if Blueled.is_lit:
        Blueled.off()
        ledBlueButton["text"] = "Turn blue LED on"
    else:
        Blueled.on()
        ledBlueButton["text"] = "Turn blue LED off"

def toggleExit():
    RPi.GPIO.cleanup()
    win.destroy()
    

ledRedButton = Button(win, text = "Red LED on", font = myFont, command = redLedToggle, bg = 'red', height = 1, width = 27)
ledRedButton.grid(row=0,column=1)

ledGreenButton = Button(win, text = "Green LED on", font = myFont, command = greenLedToggle, bg = 'green', height = 1, width = 27)
ledGreenButton.grid(row=1,column=1)

ledBlueButton = Button(win, text = "Blue LED on", font = myFont, command = blueLedToggle, bg = 'blue', height = 1, width = 27)
ledBlueButton.grid(row=2,column=1)

exitButton = Button(win, text = "Exit", font = myFont, command = toggleExit, bg = 'white', height = 1, width = 27)
exitButton.grid(row=3,column=1)
