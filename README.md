# Automatic-Defect-Inspection-of-Solar-Farm  
[Reference taken from Intel's similar work]  
  
Problem Definitions:  
To implement Image segmentation with deep learning to classify between faulty and normal solar plates images.  
  
Background:  
A solar farm, which is referred to as a photovoltaic power station, is a large-scale photovoltaic system designed for the supply of merchant power into the electricity grid. To ensure the efficiency of power output, solar farms are usually far away from cities, and sited in agricultural areas with complex terrains. Routine inspection and maintenance is a herculean task for solar farms. The traditional manual inspection method can only support the inspection frequency of once in three months. Because of the hostile environment, solar panels may have defects; broken solar panel units reduce the power output efficiency. Moreover, according to the U.S. Department of Labor, utility inspection worker is one of the top ten most dangerous jobs in the United States. So, how to improve the inspection efficiency and keep workers safe at the same time is the big challenge.  
  
<img src="/Dataset/ref/solar1.jpg">  
  
The automatic defect inspection system based on the deep learning framework developed by the team can greatly improve the efficiency for data analysis, and reduce the workload of skilled workers. Usually, most of the deep learning workloads are accelerated with graphics processing units.  
  
Solutions:  
In the solar farm panel defect inspection system, the team uses the MobileNet object detection model, using the tensorflow framework. This model can detect an object's location, size, and type.  
  
The training process is supervised learning. The number of sample images for training is very limited due to lacking real captured images from UAVs. In order to use a limited training set to ensure the high accuracy and robustness of the model, we used the dataset augmentation and ensemble method in our solution. We took about 30 original solar panel images captured from internet as input, labelled them as either passed or had defects, and also marked the positions of the defects. The image size is 224 x 224. You can follow Below link/page to know about approach  

Image Classification model using Convolutional Neural Network-Deep Learning [Link](https://github.com/RonakDedhiya/Automatic-Defect-Inspection-of-Solar-Farm/tree/master/Image%20Classification%20by%20conv2D)      
Tensorflow Object Detection API [Link](https://github.com/RonakDedhiya/Automatic-Defect-Inspection-of-Solar-Farm/tree/master/Tensorflow%20Object%20Detection%20API)    
    
Results:  
  
To illustrate the inspection effect of this system, the following sample images are shown. The image shown on the left is the original thermal image captured by UAVs obtained from internet. The image shown on the right is the detection result obtained from this inspection system. We can see that the classification and detection results are very accurate in this sample. Meanwhile, the confidence ratio of inspection results also provides valuable information for other decision-making systems in the subsequent process.  

<img src="/Dataset/ref/solar2.jpg" height="256" width="256">  <img src="/Dataset/ref/solar3.png" height="256" width="256">  
  
In this application case, utility workers would use the inspection report to guide the engineering team to change the bad units of solar panels. We cannot replace only the exact broken part of the solar panel; the solar panel should usually be replaced as a whole. That’s why end users care more about the detection rate—whether there are defects in this solar panel.  
  
Conclusion:  
  
This automatic defect inspection application for solar farms demonstrates that deep learning technology can be applied to solve real-world problems, such as unmanned inspection in harsh or dangerous environments7. The architecture of MobileNet can learn the sophisticated features from the input images for classification and detection tasks. This is a general solution for numerous inspection services in the markets, which can be used for oil and gas inspection, such as pipeline seepage and leakage; utilities inspection, like transmission lines and substations; and even for crisis response to emergencies. The UAVs can fly high up for close-up inspections without putting workers in danger. And the automatic defect inspection system can greatly improve the efficiency of mass data analysis without the help of skilled workers.  

