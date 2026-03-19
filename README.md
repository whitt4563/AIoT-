# AIoT-
라즈베리파이를 이용한 신호등 만들기

from gpiozero import LED
from time import sleep

carLedRed = 2 
carLedYellow = 3 
carLedGreen = 4
humanLedRed = 20
humanLedGreen = 21

carLedRed = LED(2)
carLedYellow = LED(3)
carLedGreen = LED(4)
humanLedRed = LED(20)
humanLedGreen = LED(21)

try:
    while True:
        carLedRed.value = 0
        carLedYellow.value = 0
        carLedGreen.value = 1
        humanLedRed.value = 1
        humanLedGreen.value = 0
        sleep(3.0)
        carLedRed.value = 0
        carLedYellow.value = 1
        carLedGreen.value = 0
        humanLedRed.value = 1
        humanLedGreen.value = 0
        sleep(1.0)
        carLedRed.value = 1
        carLedYellow.value = 0
        carLedGreen.value = 0
        humanLedRed.value = 0
        humanLedGreen.value = 1
        sleep(3.0)

except KeyboardInterrupt:
    pass

# 종료 시 모든 LED 끄기
carLedRed.off()
carLedYellow.off()
carLedGreen.off()
humanLedRed.off()
humanLedGreen.off()
