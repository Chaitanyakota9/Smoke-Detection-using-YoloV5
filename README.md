# Jetson_SDS
SMOKE DETECTION SYSTEM. a deep learning model developed on Yolov5 .It is trained and deployed on NVIDIA Jetson Nano kit

## Custom Object Detection(YOLOV5)

### Setting up Jetson Nano Kit:
 follow the page provided by Nvidia for quick setup:
 
 https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit
 
### Deepstream Installation:
Deepstream 6.0(most stable version we found):

https://docs.nvidia.com/metropolis/deepstream/6.0/dev-guide/text/DS_Quickstart.html

### Upgrading up Python 3.9

https://www.itsupportwale.com/blog/how-to-upgrade-to-python-3-9-0-on-ubuntu-18-04-lts/

### DATASET

https://drive.google.com/file/d/1sAoc-ObRKzB3ge7CJS76sm8_RbzKxXss/view?usp=sharing

### Setting up Yolov5:
https://github.com/ultralytics/yolov5

### Training the model:
Open a new google colab notebook in any browser
upload the dataset to the colab environment(you can use drag and drop)

Change the yaml file according to the classes of the data we have, and change the location of train and valid
Yaml file can be found at Yolov5/data/coco128.yaml  (OR)
replace coco128.yaml file with our data.yaml

The Source code of yolov5 algorithm to train the model is attached within this repo.
Choose your batch size and number of epochs based on the size of your training data.
After training, download best.pt file.
### Testing the model:

#### Detect.py:
open the terminal and clone the yoloV5 repository from ultralytics using following command:
 
 git clone https://github.com/ultralytics/yolov5
 
If git is not installed in your system, install it using the below command:
     sudo apt-get update
     sudo apt-get upgrade
     sudo apt-get install git
Now navigate to yolov5 directory and open requirements.txt file using following commands in terminal:

     cd yolov5
     vi requirements.txt
Edit the following lines. Here you need to press i first to enter editing mode,then make changes as below. Press ESC, then type :wq to save and quit:

     matplotlib==3.2.2
     numpy==1.19.4
     # torch>=1.7.0
     # torchvision>=0.8.1

Now copy the best.pt file into yolov5 directory.
open terminal and enter:

    python3 detect.py --weights best.pt --source 0
                                              0,1,2 -camera
                                              
                                              img.jpg
                                              
                                              video.mp4
                                              
                                              url
The custom object detection will be successfully performed by the model.

### Live Inference(Camera) on Jetson: 

Now let us try do deploy the model into DEEPSTREAM.

#### Generating weigths
1.Clone the Deepstrean-Yolo Repository

2.go to Deepstream-Yolo/utils/

3.copy gen_wts_YoloV5.py and paste to Yolov5 repo

4.enter the following command in the terminal for generating weights and cfg file:

        python3 gen_wts_yoloV5.py -w best.pt
5.create a folder for inference

6.Copy  generated weights and config files and paste the in yolov5

7.copy and paste deepstream config files into the folder created

8. Edit the config files accordingly

Run the Deepstream-app using following command:

        sudo deepstream-app -c _config.txt

## Output:

### Image Inference:
![smoke_inference_1](https://user-images.githubusercontent.com/96180326/191325495-2c1c2dfb-331e-45c1-91d6-1f5f7894eab2.jpeg)
![smoke_inference_2](https://user-images.githubusercontent.com/96180326/191325546-b1146dcc-7b68-4931-9cae-a3c30aaeb865.jpeg)
![smoke_inference_3](https://user-images.githubusercontent.com/96180326/191325564-d6395a29-46c7-4c7b-9b17-90565d9ae4a4.jpeg)
![smoke_inference_4](https://user-images.githubusercontent.com/96180326/191325579-a1b68f90-c6b3-40ef-89fe-d97d4e5bb515.jpeg)






