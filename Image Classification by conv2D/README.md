# Image Classification model using Convolutional Neural Network-Deep Learning 
  
We will be building a convolutional neural network that will be trained on images of faulty and normal, and later be able to predict if the given image is either of a fault or nofault.
  
we will be solving an image classification problem, where our goal will be to tell which class the input image belongs to. The way we are going to achieve it is by training an artificial neural network on few thousand images of fault and nofault and make the NN(Neural Network) learn to predict which class the image belongs to, next time it sees an image having a fault and nofault in it.  

we are using Keras deep learning library in python to build our CNN(Convolutional Neural Network)  
  
Preparing Dataset:  
Prepare two folders named “ test_set” and “training_set” into your working directory, it may take a while as there are nearly 500 images in both folders, which is the training data as well as the test dataset. Make sure to create a new directory and name it “dataset” and paste the above downloaded dataset folders into it.  
  
First, the folder “training_set” contains two sub folders fault and nofault, each holding 500 images of the respective category. Second, the folder “test_set” contains two sub folders fault and nofault, each holding 500 images of respective category.  
  
Building Model:    
  
The process of building a Convolutional Neural Network always involves four major steps.  
  
Step - 1 : Convolution  
Step - 2 : Pooling  
Step - 3 : Flattening  
Step - 4 : Full connection  
  