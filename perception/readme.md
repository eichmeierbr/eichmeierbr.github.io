# Perception

[Return Home](/../../)

## Computer Vision Assignments

### Bag of Words - Scene Recognition using Filter Banks

This project uses a classical approach to scene recognition. The first step uses different filters (gaussian, derivative of gaussian, etc.) at different scales to create a bank of filtered images. 

 <img align=center src="images/bag_of_words/filter_bank.png" />

Then, a feature vector is created by creating a “pipe” of a random subset of pixels through all of the images. Using a sample of these feature vectors from the training images, I used a K-means cluster to define a number of different visual words within the images. The next four pairs of images show a visual word representation of an aquarium, kitchen, waterfall, and desert respectively. 

<p float="center">
  <img src="images/bag_of_words/aquarium.png" width="400" />
  <img src="images/bag_of_words/aquarium_wordmap.png" width="400" /> 
</p>

<p float="center">
  <img src="images/bag_of_words/kitchen.png" width="400" />
  <img src="images/bag_of_words/kitchen_wordmap.png" width="400" /> 
</p>

<p float="center">
  <img src="images/bag_of_words/waterfall.png" width="400" />
  <img src="images/bag_of_words/waterfall_wordmap.png" width="400" /> 
</p>

<p float="center">
  <img src="images/bag_of_words/desert.png" width="400" />
  <img src="images/bag_of_words/desert_wordmap.png" width="400" /> 
</p>

After computing the words in an image, I use a spatial pyramid to create a histogram of the frequency of words occurring at different locations in the image. I then compare the spatial histogram to the histogram representation of each image in the training data and assign the class of the scene to the most similar histogram. This approach to scene recognition reached about a 65% accuracy when selecting between eight classes.


### Homography: Panoramas and Augmented Reality

This project used classical feature detection and matching to create a homography between a template image and a scene. I used the FAST feature detector and the BRIEF feature descriptor to locate and correlate features between two images.

![Feature Matching](images/homography/feature_matching.png)

Using these correspondences, I found the homography between both images using the following procedure:

In general, a homography correlates points on two different planes through a linear operation

<a href="https://www.codecogs.com/eqnedit.php?latex=P_1=HP_2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P_1=HP_2" title="P_1=HP_2" /></a>

where

<a href="https://www.codecogs.com/eqnedit.php?latex=P_i=&space;\begin{bmatrix}&space;x_i\\&space;y_i\\&space;1&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P_i=&space;\begin{bmatrix}&space;x_i\\&space;y_i\\&space;1&space;\end{bmatrix}" title="P_i= \begin{bmatrix} x_i\\ y_i\\ 1 \end{bmatrix}" /></a>

The H matrix is a 3x3 matrix with 8 degrees of freedom. This means we can solve the homography using 4 corresponding point pairs. To make the homography calculation robust, I employ the RANSAC algorithm to mitigate the effect of noise.

After finding the homography between the template book cover and the scene shown in the previous image, I superimpose another book cover into the scene.

<p align="center">
  <img align="center" src="images/homography/harry_potter.png" />
</p>

Using this same homography algorithm, there's two fun applications I implemented. The first algorithm is a basic panorama creator. It works by taking two images that have some amount of overlap and match the common features. Then it finds a homography from one image to the other. Improvements could be made to the panorama by blurring the boundaries between the two images. Here is a panorama I made myself using this method. The images were taken on the bridge connecting Newell Simon Hall and Wean Hall at Carnegie Mellon University. The background shows the Cathedral of Learning at the University of Pittsburgh.

<p float="center">
  <img src="images/homography/pano_left.jpg" width="400" />
  <img src="images/homography/pano_right.jpg" width="400" /> 
</p>

<p float="center">
  <img src="images/homography/full_pano.png" />
</p>

The second fun application is a basic augmented reality application. In this program I embed one video inside of another. The main video shows a scene of books, including the template book shown in the feature matching image. The second video is from Kung Fu Panda. For each frame of the book image I locate the template book and replace its area within the frame with a frame from the movie.

<p float="center">
  <img src="images/homography/panda_ar.gif" />
</p>

### Feature Tracking - The Lukas-Kanade Algorithm

In this project I made my own implementation of the Lukas Kanade tracking algorithm. I then made modern improvements to the algorithm using template correction and the inverse composition approach to estimating the template warp between frames. I evaluated the implementation on two different scenes, a car and a girl with a scooter. Both scenes assume the template only changes in position and is constant in size and shape. The red rectangle shows the tracking with template correction; the blue does not have template correction.

<p float="center">
  <img src="images/tracking/car.gif" width="400" />
  <img src="images/tracking/girl.gif" width="400" /> 
</p>

Next, I slightly modified the algorithm to find moving objects within a scene. I did this by using the entire previous frame through the sequence as the template and finding the warp from one frame to the next. Then, I determine the moving objects in the scene by computing if the difference in each pixel between the two images is above a certain threshold. The following two gifs show a scene of moving ants and driving cars respectively. Note the camera in the car sequence is moving throughout the sequence and the algorithm mostly only detects the moving objects in the scene.

<p float="center">
  <img src="images/tracking/ant.gif" width="400" />
  <img src="images/tracking/aerial.gif" width="400" /> 
</p>

### 3D Reconstruction

This project creates a 3D point cloud from two images of the same object. The following sequence of images reconstructs an ancient temple in 3D using two images taken at a slightly different perspective from the camera. Beyond documenting historical artifacts, 3D reconstruction has extensive application in SLAM/Visual Odometry.

<p float="center">
  <img src="images/reconstruction/im1.png" width="400" />
  <img src="images/reconstruction/im2.png" width="400" /> 
</p>

The first step in this process is finding the correspondences between the two images. For this project I was given the points to create the reconstruction, but they could just as easily be found using a feature matching method similar to the one I used in the homography project. Then I calculate the fundamental matrix using the 8-point algorithm. Given any point in one image, the fundamental finds the epipolar line along with that point resides in the other image. I then scan along that epipolar line to find the corresponding point in the other image.

<p float="center">
  <img src="images/reconstruction/epipolarMatch.png" />
</p>

Given the fundamental matrix, the relative camera matrices between the two images can be computed. Using the point correspondences and the relative matrices I performed a least squares error minimization to find the most likely 3D point for each given correspondence pair. The next image shows the reconstructed temple in 3D.

<p float="center">
  <img src="images/reconstruction/2temples.png" />
</p>

An application of this reconstruction is finding the position of a car in 3D space. To demonstrate this functionality, I received images from the the paper "CarFusion: Combining Point Tracking and Part Detection for Dynamic 3D Reconstruction of Vehicles" by N Dinesh Reddy, Minh Vo, and Srinivasa G. Narasimhan. This paper reconstructs the positions of cars driving through an intersection using three uncalibrated cameras. Using three concurrent images from their work, I find the location of the vehicle in the intersection relative to the first camera. The next image shows the reconstruction from two image trios.


<p float="center">
  <img src="images/reconstruction/cars.png" />
</p>

### Image Recognition with Neural Networks

In this project I implemented a fully connected neural network. I implemented the network to be modular in number of layers, nodes per layer, and activation function. I then trained the network to classify handwritten characters using the MNIST dataset. Finally, I created an algorithm to read in a full image of handwritten text, segment each of the letters, and use the network to convert the handwritten characters to text. 


<p float="center">
  <img src="images/learning/todoList.png" />
</p>

Prediction Accuracy: 87%

T0 DO LIST

I N2EE A TDDD LIST

2 CH2CK DFE THE FIRST

THING 0N TODO LIST

3 R2ALIZE YOU HAVE ALREADT

COM8LETED Z JHINGS

4 REWARD YOURSELF WITR

A NAP


<p float="center">
  <img src="images/learning/haiku.png" />
</p>

Prediction Accuracy: 89%

HAIKUS ARE EASY

BUT SQMETIMES TREX DDNT MAKE SENGE

RBFRI GERATOR


<p float="center">
  <img src="images/learning/deepLearning.png" />
</p>

Prediction Accuracy: 95%

DEEP LEARMING

DEEPER LEARNING

DEEPESP LEARNING

<p float="center">
  <img src="images/learning/alphabet.png" />
</p>

Prediction Accuracy: 75%

2BCDEFG

HIJKLMN

OPQRSTU

VWXYZ

1 Z3GSGJIJJ

Using the same neural network implementation, I also trained a 4 layer auto encoder to compress a vector from 1024 floating point values to 32, then reconstruct the input letter from the compressed data. The following images show my results on the letters M, N, O, and P.

<p float="center">
  <img src="images/learning/ms.png" width="400" />
  <img src="images/learning/ns.png" width="400" /> 
</p>
<p float="center">
  <img src="images/learning/os.png" width="400" />
  <img src="images/learning/ps.png" width="400" /> 
</p>


### Photometric Stereo

In this project I use 7 different images to reconstruct the shape of a women's face. Each of the images is taken at the same angle, but light shines on the face from a different angle. To do so, I extract the luminance channel from each image. Then, I estimate the pseudonormals of the surface in a least squares sense using singular value decomposition. I then normalize the psuedonormal at each pixel to find the pixel's albedo. The left image shows the image albedos and the right image shows the normals.

<p float="center">
  <img src="images/photometricStereo/uncalibrated_albedo.png" width="400" />
  <img src="images/photometricStereo/uncalibrated_normals.png" width="400" /> 
</p>

Finally, I integrate the matrix of psuedonormals using the Frankot-Chellappa algorithm to reconstruct the facial shape within the image. Careful application of this algorithm allows the face to be reconstructed even when the angle of the incident light rays is uncalibrated. This image shows the uncalibrated reconstruction of the face using the previous albedo and normal data.

<p float="center">
  <img src="images/photometricStereo/uncalibrated_face.png" />
</p>

## Other Learning Projects with Object Detection

### Custom YOLO

In this project I trained a custom network on top of YOLO/Darknet to detect three random objects from my living room: a rubik's cube, a cactus, and a can of my wife's favorite "hotchocky" (hot chocolate). I then ran the network live on my computer's webcam to show the results. Pardon the delays in the video, my laptop at the time was quite slow.

<p float="center">
  <img src="images/customYOLO.gif" />
</p>

### Bee Recognition

While I was at Utah State University, I too an Intelligent Systems (Intro to AI) course from Dr. Vladimir Kulyukin. The first portion of the course focused on machine learning with an emphasis on neural networks. Dr. Kulyukin maintains a beehive for research involving applying machine learning to hive monitoring. For the mid-semester project, I used neural networks, both fully connected and convolutional, for image and audio sample classification. The images were taken directly from a Raspberry Pi-Cam that performed motion detection on the hive; I trained the networks to determine the presence of a bee in the image. I also trained networks to classify audio samples of bees buzzing, crickets chirping, and background noise.

The following tables show my training results. You can also read my first attempt at writing a machine learning report [Here](images/beeRecognition.pdf):

| Architecture | Bee | No Bee |
| --- | --- | --- |
| Fully-Connected | 88% | 90% |
| Convolutional | 94.5% | 92.5% |


| Architecture | Bee | Cricket | Background |
| --- | --- | --- | --- | 
| Fully-Connected | 0.04% | 99% | 67.6% |
| Convolutional | 0.1% | 95.6% | 65.4% |

Dr. Kulyukin has since published several papers on his reasearch:

[On Video Analysis of Omnidirectional Bee Traffic Counting Bee Motions with Motion Detection and Image Classification](https://www.researchgate.net/publication/335694732_On_Video_Analysis_of_Omnidirectional_Bee_Traffic_Counting_Bee_Motions_with_Motion_Detection_and_Image_Classification)

[Toward Audio Beehive Monitoring Deep Learning vs Standard Machine Learning in Classifying Beehive Audio Samples](https://www.researchgate.net/publication/327478653_Toward_Audio_Beehive_Monitoring_Deep_Learning_vs_Standard_Machine_Learning_in_Classifying_Beehive_Audio_Samples)

[Return Home](/../../)
