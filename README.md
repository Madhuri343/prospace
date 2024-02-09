# prospace
Terrastack: Satellite Agri-Modeling

 
I wanted to classify images based on their intensity or distribution of green color into classes : no_crop,growing and lush. 
To understand the distribution of colors and extract color based features in the images i drew  histrograms.
I got L shaped curve for hue histogram which indicates that image is predominantly composed of single color or narrow range of colors.
I defined a range of (rgb) values for green color, then calculated  number of pixels in the image, calculated gratio by dividing with total pixels of the image,tried classifying images based on their gratio values but failed as images were not clear and i couldnt find best lower and upper bounds of the range of green color present in the images.

I found histogram features, loaded into a vector, it has information about the hue, saturation values after converting image from bgr color space to hsv color space
I drew color histgram features for some random images and noticed the differences in them. I loaded all of the histogram features into a list, converted into an np array and gave it as an input to kmeans clustering algorithm to classify the corresponding feature vectors into 3 classes.
I annoted the labels 0,1,2 as no_crop , grownig and lush respectively after looking at 10 images from each label. lush was easily distinguishable but no_crop and growing were not distinctly classified by my kmeans algorithm, this could be a potential error when my model will be tested with unseen images.
I created a csv file with image paths and corresponding labels obtained from kmeans clustering.
I loaded images from those image paths, gave its histogram features as inputs to a random forest classifier after encoding the output labels. I got a very poor accuracy of 42%, precision and recall for labels 1, 2 are 0, that means my model failed to predict even a single image from those models correctly.
Number of labels of each type were not almost the same so thought reason might be undersampling, created another dataset with equal labels from each type but couldnt figure the error.
I then used a cnn model to classify those images, I loaded images from the images paths present in csv file, resized and normalised them, one-hot encoded the output labels, initially I used one convolution layer, one pooling layer then a fully connected hidden layer and an output layer with relu and softmax activation functions. I used dropouts to avoid overfitting in the model.I ran it for 5 epochs initially and got an accuracy of 87% on test data. Precision, recall and f1 score was high for all the labels indicating my model predicted most of the positive instances correctly.
Next I used 2 convolution layers, and increased the number of epochs to 10, this increased my test accuracy to 92% with minimum loss.

