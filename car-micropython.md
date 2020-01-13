# Coche micro:bit

|Dispositivo|Pin
|---|---
|Neopixel| P16
|Ultrasonido Trig|P14
|Ultrasonido Echo|P15
|Sensor obstáculos| P3
|Sensor Infrarrojo y 38kHz ¿invertida? | P9
|



Según la [extensión de makeblock](https://github.com/javacasm/yahboom_mbit_en) usa un controlador de servos pca9685
( 16-channel, 12-bit PWM chip the pca9685)
con dirección  PCA9685_ADD = 0x41

https://micropython-pca9685.readthedocs.io/en/latest/
https://github.com/adafruit/micropython-adafruit-pca9685
(Adafruit usa la dirección 0x40)

Los 12bits dan para 0-4095, por lo que si usamos los 0-255 hay que multiplicar por 16

|nombre|salida
|---|---
|0| R Led RGB
|1| G Led RGB
|2| B Led RGB
|3| Servo 1
|4| Servo 2
|5| Servo 3
|6| Led Siguelineas R
|7| Led Siguelineas R
|8| Led obstaculos
|9|
|10|
|11|
|12|1/2 Motor L
|13|2/2 Motor L
|14|2/2 Motor R
|15|1/2 Motor R

Los motores conectados a los pines 12/13 y 14/15

def adelante(speedL,speedR):
    setPwm(12, 0, speedL)
    setPwm(13, 0, 0)
    setPwm(15, 0, speed2R)
    setPwm(14, 0, 0)
    
    
def atras(speedL,speedR):
    setPwm(13, 0, speedL)
    setPwm(12, 0, 0)
    setPwm(14, 0, speed2R)
    setPwm(15, 0, 0)


Led RGB grandes (convirtiendo los colores x 16)

def setRGB1(R,G,B):
    setPwm(0, 0, R)
    setPwm(1, 0, G)
    setPwm(2, 0, B) 

def setRGB2(R,G,B):
    setPwm(0, 0, R)
    setPwm(1, 0, G)
    setPwm(2, 0, B) 
    

Servos 1-3, grados 0-180

def servo(eServo, grados):
    // 50hz: 20,000 us
    let us = (grados * 1800 / 180 + 600); // 0.6 ~ 2.4
    let pwm = us * 4096 / 20000
    setPwm(eServo + 2, 0, pwm)
    
# Sensores de linea analogicos P2 (left) P1 (right)
# que activan los leds conectados a 7 y a 6 
