# Perception

## CV Assignments

### Bag of Words - Scene Recognition using Filter Banks

This project uses a classical approach to scene recognition. The first step uses different filters (guassion, derivative of gaussian, etc.) at different scales to create a bank of filtered images. 

#### Filter Bank Images go Here

Then, a feature vector is created by creating a “pipe” of a random subset of pixels through all of the images. Using a sample of these feature vectors from the training images, I used a K-means cluster to define a number of different visual wors within the images. The next four pairs of images show a visual word representation of an aquarium, kitchen, waterfall, and desert respectively. 


#### Different Scenes go here


After computing the words in an image, I use a spatial pyramid to create a histogram of the frequency of words occurring at different locations in the image. I then compare the spatial histogram to the histogram representation of each image in the training data and assign the class of the scene to the most similar histogram. This approach to scene recognition reached about a 65% accuracy when selecting between eight classes.


### Homography: Panoramas and Augmented Reality

This project used classical feature detection and matching to create a homography between a template image and a scene. I used the FAST feature detector and the BRIEF feature descriptor to locate and correlate features between two images.

#### Feature matching goes here

Using these correspondences, I found the homography between both images using the following procedure:

In general, a homography correlates points on two different planes through a linear operation

<a href="https://www.codecogs.com/eqnedit.php?latex=P_1=HP_2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P_1=HP_2" title="P_1=HP_2" /></a>

where

<a href="https://www.codecogs.com/eqnedit.php?latex=P_i=&space;\begin{bmatrix}&space;x_i\\&space;y_i\\&space;1&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P_i=&space;\begin{bmatrix}&space;x_i\\&space;y_i\\&space;1&space;\end{bmatrix}" title="P_i= \begin{bmatrix} x_i\\ y_i\\ 1 \end{bmatrix}" /></a>

The H matrix is a 3x3 matrix with 8 degrees of freedom. This means we can solve the homography using 4 corresponding point pairs. To make the homography calculation robust, I employ the RANSAC algorithm to mitigate the effect of noise.

After finding the homography between the template book cover and the scene shown in the previous image, I superimpose another book cover into the scene.

#### HP Book Cover


