This is a shortened documentation of my undergraduate thesis—Keyword Spotting Using Convolutional Neural Network on Microcontroller-based Board as a Smart Switch for Devices. Basically, the prototype provided in the thesis is a voice-controlled smart switch for two devices. The trigger keywords are _one_, _two_, _on_, and _off_. _One_ and _two_ are used to switch between the two devices, while _on_ and _off_, quite intuitively, are used to turn the devices on or off. Here is a [demonstration video](https://www.youtube.com/watch?v=_5sMkls3ZtQ) of the prototype.

Proceeding to the discussion of terms for easier discussion, keyword spotting (KWS) is a machine learning algorithm that is used to detect certain keywords from a stream of live audio. As for convolutional neural network (CNN), it is used in KWS to classify the keywords, CNN is a deep learning architecture commonly used for image classification. Lastly, microcontroller (MCU) is an embedded device found in almost all of commonly used electronic gadget, it can be simply described as a less-powerful  miniature version of a computer. Arduino is a common development board that uses microcontroller.

# Materials
---
### Arduino Nano 33 BLE Sense
Arduino Nano 33 BLE Sense (Arduino 33) is an AI-enabled board—where AI-enabled means that it is compatible with existing AI software tools such as TensorFlow Lite for Microcontroller and Edge Impulse, etc.—operating at 3.3 V. It has multiple built-in sensors such as 9-axis inertial sensor, humidity and temperature sensor, barometric sensor, microphone, gesture sensor, proximity sensor, and light color and intensity sensor. It also has a Bluetooth Low Energy (BLE) chipset and can also be used as a Bluetooth host and client [1]. The pin diagram of Arduino 33 is shown below.

![image](https://user-images.githubusercontent.com/94373003/179490551-f4febdad-93bc-42f6-8bca-51ceafca4557.png)

Photo from [1]

---
# Methods
---
### Machine Learning Design
---


###
---
#### Keyword Spotting
---
#### IMU
---
# References
[1] https://store-usa.arduino.cc/products/arduino-nano-33-ble-sense
[2]

Since audio is a 1D signal and images are 2D, feature extraction is first performed on audio to convert it into 2D signal. One sample of algorithm used




