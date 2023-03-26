# Speech Recognition Using Tiny Machine Learning (Tiny-ML) on Different Edge Devices (Arduino Nano 33 BLE Sense and Raspberry Pi) 


In this project, we explore the use of TinyML, a subset of machine learning that focuses on running models on small, low-power devices, for speech recognition on two different edge devices: the Raspberry Pi and the Arduino Nano 33 BLE Sense. We demonstrate the feasibility of using these devices for speech recognition by training and running a model on each platform. The results show that both devices are capable of performing speech recognition with a high level of accuracy, highlighting the potential for TinyML in speech recognition applications on edge devices. Additionally, we compare the performance and power consumption of the two devices, providing insight into the trade-offs between the two platforms. The Edge Impulse Platform was utilized with an Arduino Nano 33 BLE Sense and a 2D CNN model on a Raspberry Pi 4. The accuracy for the Arduino Nano 33 BLE Sense was 92.3% and 91% for the Raspberry Pi.
 
 
 Overall, this work demonstrates the potential of TinyML for enabling speech recognition on low-power edge devices and paves the way for further research in this area.

 ## Application Architecture Overview

![application_overview](https://user-images.githubusercontent.com/73910961/227767682-4f8d765b-d793-4b45-ba65-490dc2949613.jpg)

### Data Collection/ Dataset
![dataset](https://user-images.githubusercontent.com/73910961/227767894-24642c1c-4eef-475c-ad21-5dcef7961516.png)

Speech Commands: A Dataset for Limited-Vocabulary Speech Recognition from Pete Warden (https://arxiv.org/abs/1804.03209).

The dataset contains 35 different words. In Figure 5, the vocabulary can be seen in the dataset. Each word has many numbers of utterances as you can see in the figure. In our case, we chose “one”, “two”, “three”, “four”, “on”, and “off” words and also background noise. Totally we have 6884 samples. The samples divided such as 80% for training, %10 for validation, % and 10 for testing.

### Data Preprocessing

To work with human voices, Mel Frequency Cepstral Coefficients (MFCCs) are used to convert sound into a set of numbers that closely mimic how we perceive speech. To accomplish this, similar to before, the FFT is taken of a windowed segment of the waveforms, and a set of Mel-spaced triangular filters are created for this FFT. Then, the energy of each filter is computed. This is found by summing the area under the curve after multiplying the FFT by the filter, these energy values are stored in an array. low-frequency energies at the top and high-frequency energies at the bottom. The logarithm of each energy value is then calculated. This simulates how sound is perceived by humans. Loudness is perceived by us on a logarithmic scale rather than a linear one. The discrete cosine transform, also known as the DCT, is then applied to this set of energy values. DCT compresses the information while allowing us to decorrelate the energy values due to the overlapping filters. The MFCCs, or Mel frequency cepstral coefficients, are the result of this DCT process. The DCT produces an equal amount of output values as input values.

At the end of the MFCC process, the overall shape of the spectrogram is important. Also, we have an image for each word at the end of the MFCC process.
![mfcc_outputs](https://user-images.githubusercontent.com/73910961/227768275-4dc78ec6-ee7e-4754-ac46-ffd0f4bd6213.png)

### Design a Model 
The 2D CNN model is used.


![2d_cnn_model](https://user-images.githubusercontent.com/73910961/227768434-95b75fde-762c-495c-8113-5a1dda55d859.jpg)

### Evaluate the Performance
![training_and_validation_accuracy](https://user-images.githubusercontent.com/73910961/227768577-22ea4887-666f-47a6-977c-880d1749cae8.png)
![confusion_matrix](https://user-images.githubusercontent.com/73910961/227768681-0bf1264e-2f4d-4bdd-97c3-108950810a36.png)

### Convert the Model
Tensorflow Lite Conversion: This conversion process transforms the TensorFlow model into a version that can be used in devices with limited memory. 

### Deploy the Model 
![deploying_part](https://user-images.githubusercontent.com/73910961/227769275-55670aec-0222-4f83-b2de-6f7711bf07c3.png)




###### Raspberry Pi Deploying Process
![raspberrypi_deploying_process](https://user-images.githubusercontent.com/73910961/227768964-69a47916-62d6-4bf3-84b4-2c8f3a6f42e8.jpg)

###### Arduino 33 BLE Sense Deploying Process
Challenges in this part:
- Limited Resources Available
- Many Error Messages in Arduino code part
- Limited Memory

Because of these reasons, decided to use Edge Impulse platform in the Arduino 33 BLE Sense deploying part.

In this process, the same dataset, same data preprocessing and, same model is used with Edge Impulse Platform.

![arduino_confusion_matrix](https://user-images.githubusercontent.com/73910961/227769490-739e22c4-7f4b-4960-9353-57eaf3f80f5f.jpg)

### Comparison Results of Arduino vs Raspberry Pi

![raspberryvsarduino](https://user-images.githubusercontent.com/73910961/227769790-eb9eef2f-96d7-4392-a727-854ffbc19156.png)


### Conclusion
- Speech recognition was used on two different edge devices.
- Two different methods was used to create a model.
- Edge impulse was used for Arduino Nano 33 BLE Sense.
- Tensorflow Lite was used for Raspberry Pi.
- The next step is to design a voice assistant application that works with edge devices.

### References
[1] TinyMLx.Harvard TinyML Course.[Online]: 
Available: https://www.edx.org/professional-certificate/harvardx-tiny-machine-learning

[2] Pete Warden, Speech Commands: A Dataset for Limited-Vocabulary Speech Recognition, April 2018.







