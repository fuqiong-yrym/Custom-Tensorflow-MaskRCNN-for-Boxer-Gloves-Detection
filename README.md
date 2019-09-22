# Tensorflow-Object-Detection-API-to-Detect-Boxing-Gloves-

Tensorflow object detection API provides convenient tools to do object detection and instance segmentation which are two main tasks in computer vision. The equipped [model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md) includes popular algorithms like ssd, faster rcnn, mask rcnn (for both bounding box & mask detection), with a variety of effective feature detectors like mobine net, resnet and inception resnet. The tradeoff between speed and accuracy of these models is thoroughly studied in this [paper](https://arxiv.org/pdf/1611.10012.pdf). Users can select a proper model as needed. The API provides easy-folowed pipeline to customize inputs, model parameters and evaluation metrics. The model training can be easily deployed on google cloud, with some supported by TPU. 

In this repository, I used tensorflow object detection API to do a very interesting job -- trying to detect boxing gloves and segment them during the boxers are fighting or training. The results can help us better appreciate the trajectory of boxing moves. Eventually, a set of continued frame images from a short video is displayed with the detected bounding boxes as well as masks for presented gloves. The training was done on google cloud.

The repository includes:

* Jupyter notebooks to visualize the detection on images
* Jupyter notebooks to visualize the detection on video

# Inputs Preparation:

* **Labeling:** Prepare images and annotations for training, evaluation and testing. The label tool selected is RectLabel for mac. RectLabel is simple and easy to use, also very handy since it has attracting features such as exporting compatible annotation formats, automatically generating label map, separating datasets and producing file list which are all required when using tensorflow detection API. In this example, training set contains ~150 images. 

<p align="center">
  <img src="/test_images/23.jpg" width=676 height=450 />
</p>

<p float="left">
  <img src="/23_pixels0.png" width="100" /> 
  <img src="/23_pixels1.png" width="100" />
  <img src="/23_pixels2.png" width="100" />
  <img src="/23_pixels3.png" width="100" />
 </p>

* **Inputs:** Convert images and annotations into TFRecord format. The masks were included. Tensorflow API provides sample tools to do this conversion. According to the annotation format (PASCAL, Coco, KITTI) choose the corresponding tool. You may need make some changes if the format in your hand does not fall into the provided ones. 
(consider whether to post the conversion tool...)

* **Configuration:** Prepare config file for the model. I modified the config sample provided by Tensorflow API to change two basic things: 1. number of output, 2. paths to files used for training and evaluation. These two places are a must to change when you uses your own datasets, otherwise errors are expected. This config file also allows you to set the checkpoint file from which the training starts. I used faster rcnn reset101 trained on COCO. 

<p align="center">
  <img src="readme.png" width=676 height=450>
</p>

![Boxing fight video clip](Boxing_fight_readme_downsize.gif)


<p align='center'>
  <img width="600" height="338" src="Boxing_fight_readme_downsize.gif">
</p>

