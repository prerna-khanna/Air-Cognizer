[![](https://img.youtube.com/vi/sBTqLHA95rs/0.jpg)](https://www.youtube.com/watch?v=sBTqLHA95rs)

# Air Cognizer: Predicting Air Quality with Smartphone Camera Images
## Inspiration
Large cities like Delhi can suffer from air pollution, especially in winter, and we’ve seen headlines like **“Cold Morning In Delhi, Air Quality Continues To Be Severe”** appear on the front page of newspapers.
As engineering students, we strive to use technology for social good. A crucial first step in solving the air pollution problem is to **enable citizens to gauge the quality of air they breathe**.

This could be done with pollution sensors — although they can be expensive to deploy at scale. Our goal was to develop an Android-based mobile application to provide inexpensive, localized and real-time air quality estimation using smartphone camera images.

## What it does
The application we developed collects images from the camera on the mobile phone, and processes them on-device to extract a few image based features, then using TensorFlow Lite these features provide an Air Quality Index (AQI) estimate.

## How we built it
First we prepared a data set of 5000 images captured in Delhi with their ground truth as the AQI levels measured from portable air quality meter. 
Next we extracted image features like Blue color of the sky, Gradient of sky region, ROI contrast, Transmission, Entropy which were relating to AQI.
Then we trained an **Image based AQI estimation model** on cloud. 

We describe the system in detail below:
1. **The Mobile Application**. This is used to capture images and predict AQI levels. The application processes images on-device.
2. **TensorFlow Lite** is used to power on-device inference, in a small binary size (which is important for download speed, when bandwidth is limited) for the trained machine learning model.
3. **Firebase**. Parameters extracted from the images (described below) are sent to Firebase. Whenever a new user uses the app, a unique ID is created for them. This can be used later to customize the machine-learning model for different geo-locations and variety of smartphone cameras.
4. **Amazon EC2**. We train our models here, using these parameters and the PM values from the geo-location.
5. **ML Kit**. Trained, custom models for different smartphones are hosted on ML Kit, and automatically downloaded on to the device, then run with TensorFlow Lite.

We combine the results with a temporal **Meteorological Parameter based model** which has inputs to it as: concentration of gases like SO2, C02, O3 and humidity of the users' location.
This helps achieve higher inference accuracy and give reliable results to the user while the image-based machine learning model is being trained.

![System Architecture](https://user-images.githubusercontent.com/35433654/56471792-36ce8980-6474-11e9-8643-e4c834debab0.png)


## Challenges we ran into
1. **Deploying a custom model** for every device, keeping in mind the different camera specifications and providing custom updates for different users.
ML Kit solved this problem for providing custom updates and deploying these models. 

2. Initially when the application was launched people started to click images indoors to check AQI, while our model works only with a skyline.
We incorporated a **Skyline estimation model** using TensofFlow Hub by retraining the Mobile Net architecture on our our custom skyline and non skyline classes. 

## Accomplishments that we're proud of
1. The project was covered by major newspapers creating an awareness among the people.
[The Hindu. ](https://www.thehindubusinessline.com/news/science/use-your-phone-camera-for-real-time-pollution-check/article25426953.ece)
[NDTV.](https://gadgets.ndtv.com/apps/news/delhi-air-pollution-college-students-develop-app-to-measure-air-quality-1943152)

2.  Application was launched on Play Store on November 1st ’18 and was trending on 1st place during Diwali (7th 
     November) time under weather applications.  

3. We received a positive feedback and constructive appreciation from residents of Delhi through comments on Play 
    Store and mails. One of the users’ comment :

      _“When you walk out of home in Delhi, Air Quality does not seem as it is. The sky look clear and 
         shining sun don’t tell the truth. But this app tells you air quality with just one click. Thank you “_ 

## What we learned
1. During the course of our research we found that the major contributor to air pollution is construction sites and not traffic problem in Delhi, while the Govt. is still making traffic regulation norms instead of regulating construction norms.
2. In last stages of the project we realized the power of on device computing and how a tool like Machine Learning can make a difference to such a big problem. 

## What's next for Air Cognizer
We intend to make the following improvements to improve the application in future:
1. Generate results on photos taken at **night**.
2. Extend **reachability** to other major cities.
3. Make the model **robust** in various weather conditions.

## Acknowledgements
We would like to thank our mentors, Dr. Aakanksha Chowdhery and Prof. Brejesh Lall for their guidance and constant encouragement during the course of the project. We would also like to thank Marconi Society for sponsoring Celestini Project India. 

## Follow our Project
[PlayStore](https://bit.ly/AirCognizer)

[Website](https://bit.ly/Air_Cognizer)

[Blog](https://bit.ly/AirCognizerBlog)

##Authors
[Prerna Khanna](http://bit.ly/KhannaPrerna) and [Tanmay srivastava](http://bit.ly/tanmaySrivastava)

