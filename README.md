# IoT26-HW03

## Raspberry Pi Motion Detector with Photo Capture

## 1. Objective

The objective of this assignment is to use Raspberry Pi to detect motion and take photos automatically.

In this project, a PIR motion sensor detects movement. When motion is detected, the Raspberry Pi camera captures a photo and saves it as an image file.

## 2. Components

- Raspberry Pi
- PIR Motion Sensor
- Raspberry Pi Camera
- Push button
- Jumper wires

## 3. GPIO Pins

| Component | GPIO Pin |
|---|---|
| PIR Motion Sensor | GPIO4 |
| Push Button | GPIO2 |

## 4. Source Code

```python
# project updates at: https://nostarch.com/RaspberryPiProject

# import the necessary packages
from gpiozero import Button, MotionSensor
from picamera2 import Picamera2
from time import sleep
from signal import pause

# create objects that refer to a button,
# a motion sensor and the PiCamera
button = Button(2)
pir = MotionSensor(4)
camera = Picamera2()
camera.start()

# start the camera
camera.rotation = 180
# camera.start_preview()

# image image names
i = 0

# stop the camera when the pushbutton is pressed
def stop_camera():
    camera.stop_preview()
    # exit the program
    exit()

# take photo when motion is detected
def take_photo():
    global i
    i = i + 1
    camera.capture_file('/home/aiot/image_%s.jpg' % i)
    print('A photo has been taken')
    sleep(10)

# assign a function that runs when the button is pressed
button.when_pressed = stop_camera
# assign a function that runs when motion is detected
pir.when_motion = take_photo

pause()
```

## 5. How to Run

```bash
python3 HW3.py
```

## 6. Result

The PIR motion sensor detects movement through GPIO4.

When motion is detected, the Raspberry Pi camera captures a photo and saves it as an image file.

The terminal prints the message:

```text
A photo has been taken
```

This confirms that the Raspberry Pi detected motion and captured photos successfully.

## 7. Screenshots and Evidence

### Source Code Screenshot

![HW3 Code](images/hw3_code.png)

### Running Program Screenshot

![HW3 Run](images/hw3_run.png)

### Raspberry Pi Motion Sensor and Camera Setup

![HW3 Result](images/hw3_result.jpg)

### Captured Photo

![HW3 Captured Photo](images/hw3_captured_photo.jpg)

## 8. Members

- 장동현 / AI·소프트웨어학부 소프트웨어전공
- 임규민 / AI·소프트웨어학부 인공지능전공
- 이형호 / AI·소프트웨어학부 인공지능전공
