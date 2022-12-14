# ENGI 301
<h1> ENGI301
Repository for ENGI301 course work


import time
import board
import pulseio
import digitalio
from adafruit_motor import servo
from adafruit_circuitplayground import cp

# Set up the PocketBeagle
cp.pixels.brightness = 0.3
cp.play_file("audio_file.wav")

# Set up the PIR motion sensor
pir = digitalio.DigitalInOut(board.D6)
pir.direction = digitalio.Direction.INPUT

# Set up the servo motor
servo = servo.Servo(board.D10)

# Set up the vibration motor
vibration_motor = pulseio.PWMOut(board.D5, frequency=160)

# Set up the LED strip lights
led = digitalio.DigitalInOut(board.D13)
led.direction = digitalio.Direction.OUTPUT

# Main loop
while True:
    if pir.value:
        # Trigger the servo motor to rotate 90 degrees
        servo.angle = 90
        time.sleep(1)

        # Trigger the vibration motor
        vibration_motor.duty_cycle = 2**15
        time.sleep(1)

        # Flash the LED strip lights
        led.value = True
        time.sleep(0.5)
        led.value = False
        time.sleep(0.5)

        # Play the audio file
        cp.play_file("audio_file.wav")

    time.sleep(0.1)
