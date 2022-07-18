This is a shortened documentation of my undergraduate thesis—Keyword Spotting Using Convolutional Neural Network on Microcontroller-based Board as a Smart Switch for Devices. Basically, the prototype provided in the thesis is a voice-controlled smart switch for two devices. The trigger keywords are _one_, _two_, _on_, and _off_. _One_ and _two_ are used to switch between the two devices, while _on_ and _off_, quite intuitively, are used to turn the devices on or off. Here is a [demonstration video](https://www.youtube.com/watch?v=_5sMkls3ZtQ) of the prototype. For clarification, all computation is performed on board. No external processors/computers were used to perform the keyword spotting algorithm. This means that the prototype has the potential of being a smartwear device that can control multiple devices remotely, especially that the board also has a BLE chipset.

Proceeding to the discussion of terms for easier discussion, keyword spotting (KWS) is a machine learning algorithm that is used to detect certain keywords from a stream of live audio. As for convolutional neural network (CNN), it is used in KWS to classify the keywords, CNN is a deep learning architecture commonly used for image classification. Lastly, microcontroller (MCU) is an embedded device found in almost all of commonly used electronic gadget, it can be simply described as a less-powerful  miniature version of a computer. Arduino is a common development board that uses microcontroller.

# Materials
---
### Arduino Nano 33 BLE Sense
Arduino Nano 33 BLE Sense (Arduino 33) is an AI-enabled board—where AI-enabled means that it is compatible with existing AI software tools such as TensorFlow Lite for Microcontroller and Edge Impulse, etc.—operating at 3.3 V. It has multiple built-in sensors such as 9-axis inertial sensor, humidity and temperature sensor, barometric sensor, microphone, gesture sensor, proximity sensor, and light color and intensity sensor. It also has a Bluetooth Low Energy (BLE) chipset and can also be used as a Bluetooth host and client [1]. The pin diagram of Arduino 33 is shown below.

This board was selected due to its compatibility with existing Tiny Machine Learning frameworks and its availability.

![image](https://user-images.githubusercontent.com/94373003/179490551-f4febdad-93bc-42f6-8bca-51ceafca4557.png)

Photo from [1]

---
# Methods
---
#### Data Preprocessing
First off is a brief description of the data. Two datasets—speech commands dataset (SCD) v2 [2] and ESC-50 [3]—was combined in the study. Both datasets are audio/sound, with SCD created for the purpose of keyword spotting while ESC-50 for environmental classification. SCD has multiple keywords such as digits one to nine, activation words such as on and off, and some random words such as Marvin and Sheila. On the other hand, ESC-50 is a dataset composed of environmental sounds such as rain, clapping sounds, and cricket sounds.

To properly combine the datasets, ESC-50 was preprocessed as the same specifications of the SCD dataset. A script was written using python, so that ESC-50 samples are one-second length each and sampled at 16kHz. These samples were added to the _background noise_ samples of the SCD. In preparing the dataset, a script was written to separate the keywords _one_, _two_, _on_, _off_, and _background noise_ into a separate folder. Classes/labels in SCD not belonging to the prior mentioned keywords are randomly grouped into one label—_unknown_. The data distribution is uniform, each with 2500 samples, thus a total of 15,000 samples.


#### Feature Extraction
Audio is transformed into MFCC as the input to the CNN. This is done since CNN is commonly used in images (which are 2D signals) and audio is a 1D signal thus feature extraction is first performed on audio to convert it into 2D signal. Shown below is the process of MFCC conversion from audio of Edge Impulse. To extract MFCC, Edge Impulses uses SpeechPy, a Python package for extracting features from audio by Torfi [4].

![image](https://user-images.githubusercontent.com/94373003/179495237-be499050-b3e3-4427-8a09-3e38ac9509aa.png)

MFCC is a signal processing function offered by Edge Impulse which converts raw audio data into mel-frequency spectrogram. Shown below is a pictorial process of the conversion.

![image](https://user-images.githubusercontent.com/94373003/179495480-c79ff04a-7797-413f-8a10-4be8c7f62680.png)

#### CNN Model Selection
Three models are adapted for this study’s use-case. These models should have small-footprint and low computation time. The application should also be sound/voice classification. To make the process easier, CNN models that have already been deployed to Arduino 33 are more preferred as opposed to models deployed on other microcontroller-based boards.

The first model is from Waqar et al (2021), which is used for Speech Emotion Recognition (SER). The audio data is converted to MFCC, which is then used as the input for the CNN. The SER The SER application of the study is on anger classification, where they used 0.98 confidence as “angry”, 0.55 to 0.98 as “about to be angry” and less than 0.55 as “not angry”. The trained model was deployed onto Arduino 33. The model architecture is shown in Figure 3-7a.

The second model is from Amjath and Kuhanesan (2021), which is a warning system for railway track workers, they named TrackWarn. The input used for the study is also MFCC. The model is a binary classification, with 0.7 confidence to be classified as the train sounds. The trained model was deployed to Arduino 33. The architecture is shown in Figure 3-7b.

Lastly, the third model is from Trivedi and Shroff (2021), which classifies three species of mosquitoes based on the sound of their wing beats. The input used for the study is Mel-Filterbank Energy, which is like MFCC, except DCT was not performed. The trained model was deployed to Arduino 33 using Edge Impulse. The architecture is seen in Figure 3-7c.

The input shape for models is the size of the extracted MFCC, ℝ1 x 650. All the convolution layers use ReLu as the activation layer. The output of the max pooling/last convolutional layer is flattened, followed by dropout (randomly dropping nodes to address overfitting) before going to the output layer with activation of SoftMax. The optimizer to be used is based on Mittermaier et al. (2021) which is Adam optimizer, and the loss function is categorical cross entropy. 

![image](https://user-images.githubusercontent.com/94373003/179495735-62e7e38a-cebb-4873-98d6-95b57f1015b1.png)


#### Hyperparameter Optimization 

#### Model Training and Deployment via Edge Impulse

#### On-board inferencing
---
# References
[1] https://store-usa.arduino.cc/products/arduino-nano-33-ble-sense
[2] https://arxiv.org/abs/1804.03209
[3] https://dl.acm.org/doi/10.1145/2733373.2806390
[4] https://zenodo.org/record/840395







