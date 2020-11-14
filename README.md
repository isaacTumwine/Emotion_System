# Emotion_System
The model performs really well in the real world and it has an accuracy of 75% on the test data.
Datasets
The Datasets which I have used in this project are AffectNet and FER+ (which is the same as fer2013 Kaggel but with better labels)

The combination of these dataset will have about 300,000 images for the 5 class.

Class	Number of Images
Happy	134,626
Neutral	86,518
Sad	29,886
Angry	28,168
Surprise	18,608
Dependencies
numpy (1.16.4)
tensorflow (1.14.0)
keras (2.2.4)
opencv (3.4)

Haar-Cascade
Haar cascade classifiers first were proposed by Paul Viola and Michael Jones and uses Haar kernels for extracing features and it uses multiple classifiers one after an other. The classifiers get more complex as data move forward. Each classifier will specify whether the image is maybe from the desired class or it is definitly not in the desired class and if it is maybe from the desired class will pass image forward to the next classifier.

For training these classifiers,first you need to collect images from desired class (positive data in our case face images) and everything else (negative data) especially from the environment which you want to test your model like chairs, tables, etc. (for better result its better to make the images grayscale). Also you need to make a description file for postive and negetive samples.

For positives you need to write in the following format: [filename] [number of object annotations] [coordinates of the objects bounding rectangles (x, y, width, height)] for example: img/img1.jpg 1 140 100 45 45
For negative images you only need to write the file name
After collecting data and creating the two description files, you have to install opencv and its dependencies. Then using following commands you can start training your model:

First you need to create a vector file from the positive image with the following command: opencv_createsamples -info [name of description file] -num [number of positive samples] -w [width of the output] -h [height of the output] -vec [name of the vector file] for example:

opencv_createsamples -info info/info.lst -num 9000 -w 20 -h 20 -vec positives.vec

Then after creating the vector file you can start the actuall training with the following command:

opencv_traincascade -data data -vec positives.vec -bg bg.txt -numPos 7000 -numNeg 3500 -numStages 10 -w 20 -h 20

I trained the haar cascade with 7000 positive images and 3500 negative images for 21 stage which it make a very few mistakes.

For more information you can reffer to opencv website.

References
Rapid Object Detection usinga Boosted Cascade of Simple Features

AffectNet: A Database for Facial Expression, Valence, and Arousal Computing in the Wild

Kaggel Challenge
