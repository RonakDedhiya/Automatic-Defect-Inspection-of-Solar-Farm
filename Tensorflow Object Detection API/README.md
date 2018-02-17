# Tensorflow Object Detection API  
  
Problem statement :  
  
Detect the defect/fault of solar panel using machine learning and locate the fault on thermal image of solar panel.  
  
High level requirement :  
  
Python 2/3, Tensorflow >=1.4.0  
  
Implementation :  
  
Tensorflow Object Detection API is a computer vision library for object detection from image or video. In our use case we have to detect fault, here we are treating fault as an object.  
  
A brief overview of the steps needed to do this:  
  
1. Collect a few hundred images that contain your object - The bare minimum would be about 100, ideally more like 500+, but, the more images you have, the more tedious step 2 is...  
2. Annotate/label the images, ideally with a program. We used LabelImg. This process is basically drawing boxes around your object(s) in an image. The label program automatically will create an XML file that describes the object(s) in the pictures.  
3. Split this data into train/test samples  
4. Generate TF Records from these splits  
5. Setup a .config file for the model of choice (you could train your own from scratch, but we'll be using transfer learning)  
6. Train  
7. Export graph from new trained model  
8. Detect custom objects in real time!  

Image Labeling :  
Install LabelImg and annotate the image by locating fault as shown bellow:  
  
<img src="/Dataset/ref/label.png">	

By this process we are able to generate annotated xml file for each image.  
  
Once  images labeled, we're going to separate them into training and testing groups. To do this, just copy about 10% of your images and their annotation XML files to a new dir called test and then copy the remaining ones to a new dir called train.  
  
TFRecord file:  
For training we require to convert our input data in TFRecord file for this we need to do two steps. First is convert xml to csv and the make TFRecord file.
Run xml_to_csv.py to convert all xml file to one csv file which contain label information.  
Then to make TFRecord file of train data run generate_tfrecord_train.py by using command python generate_tfrecord_train.py --csv_input=data/train_labels.csv --output_path=data/train.record also for test data run generate_tfrecord_test.py by using command python generate_tfrecord_test.py --csv_input=data/test_labels.csv --output_path=data/test.record  
 Now, in your data directory, you should have train.record and test.record and for all the above steps our folder structure is  

Object-Detection  
-data/  
--test_labels.csv  
--train_labels.csv  
-images/  
--test/  
---testingimages.jpg  
--train/  
---testingimages.jpg  
--...yourimages.jpg  
-training  
-xml_to_csv.py  
-generate_tfrecord_train.py  
-generate_tfrecord_test.py  
  
Now clone https://github.com/tensorflow/models.git and follow installation steps.  
  
Now download ssd_mobilenet_v1_coco_11_06_2017.tar.gz and extranct to our Object-Detection folder.  
  
Also download and (edit if required) ssd_mobilenet_v1_pets.config   
  
Training:    
Now move content of our object detection folder to downloaded github repository in research\object_detection folder.  
Inside training directory, add object-detection.pbtxt:  
  
item {  
  id: 1  
  name: 'fault'  
}  
Now to start training, From within models/object_detection run :  
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/ssd_mobilenet_v1_pets.config  
  
  
For training it will take lot of time after loss become less than 1 then you can interrupt training.  
Testing   
In order to test our model, we need to export the inference graph. In the models/object_detection directory, there is a script that does this for us:   export_inference_graph.py To run this, you just need to pass in your checkpoint and your pipeline config, then wherever you want the inference graph to be placed. For example:   
python export_inference_graph.py \  
--input_type image_tensor \  
--pipeline_config_path training/ssd_mobilenet_v1_pets.config \  
--trained_checkpoint_prefix training/model.ckpt-10856 \  
--output_directory fault_inference_graph  
  
our checkpoint files should be in the training directory. Just look for the one with the largest step (the largest number after the dash), and that's the one you want to use. Next, make sure the pipeline_config_path is set to whatever config file you chose, and then finally choose the name for the output directory, we went with fault_inference_graph.  
  
Now, we're just going to use the sample notebook, edit it, and see how our model does on some testing images. I copied some of my models/object_detection/images/test images into the models/object_detection/test_images directory, and renamed them to be image3.jpg, image4.jpg...etc.  
  
Booting up jupyter notebook and opening the object_detection_tutorial.ipynb, let's make a few changes. First, head to the Variables section, and let's change the model name, and the paths to the checkpoint and the labels:  
  
# What model to download.  
MODEL_NAME = 'fault_inference_graph'  
  
# Path to frozen detection graph. This is the actual model that is used for the object detection.  
PATH_TO_CKPT = MODEL_NAME + '/frozen_inference_graph.pb'  
  
# List of the strings that is used to add correct label for each box.  
PATH_TO_LABELS = os.path.join('training', 'object-detection.pbtxt')  
  
NUM_CLASSES = 1  
  
Next, we can just delete the entire Download Model section, since we don't need to download anymore.  
   
Finally, in the Detection section, change the TEST_IMAGE_PATHS var to:  
TEST_IMAGE_PATHS = [ os.path.join(PATH_TO_TEST_IMAGES_DIR, 'image{}.jpg'.format(i)) for i in range(3, 8) ]  
  
With that, you can go to the Cell menu option, and then "Run All."  
  
Here are a few of our results:  
<img src="/Dataset/ref/result1.png">  
<img src="/Dataset/ref/result2.png">  
<img src="/Dataset/ref/result3.png">  

