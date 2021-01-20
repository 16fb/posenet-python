# Aims
* Figure how use PoseNet Python Implementation
* Run Python Implementation on My Computer
* Run Python Implementation on rasp pi
* Port over into container + ARM32

TODO:  
First -> Test inferencing speed on images:
* Test if conda envrionment works
* Port over to Rasp Pi, see if conda + everything works there.
* Create container to use on Atlas 500.
* Document Speed of FPS on devices.

Second -> Expand scope to work on videos / RTSP Stream:
* Test if can cv2 input from RTSP Stream
* Configure code for alternate way to display results [no monitor] (cv2.imwrite video?)
* Put everything into code



## What is this repo
Pure python implementation of PoseNet

Requirements:
* Python 3.x
* Latest version of TF
* Tested On Versions: Conda Python 3.6.8 and Tensorflow 1.12.0
* For Webcam Demo -> `pip install opencv-python` [Conda default opencv no ffpmeg support]

Suitable Conda Environment:  
```
conda install tensorflow-gpu scipy pyyaml python=3.6
pip install opencv-python==3.4.5.20
```

## Usage Image Pose
### Conda Environement
(tf)  

### Download Test Images
`python get_test_images.py`

### Run inferences on input folder of Images
`python image_demo.py --model 75 --image_dir ./images --output_dir ./output`

Results --model 101:  
* Avg 9FPS

Results --model 75:  
* Avg 12FPS


Command Prompt vs PowerShell:
* Actually roughly same speed :THINKING:

## Usage Video/Webcam Pose
### Run inferences on WebCam
`python webcam_demo.py --model 101`  

Q -> Stops webcam  

Results --model 101:  
* Avg 9FPS

Results --model 75:  
* Avg 12FPS

### Run inferences on RTSP Stream
`python ExternalCamera.py --model 101`   

Modified:  
`cap = cv2.VideoCapture("rtsp://service:sc903cam@10.4.1.253")`  


## Porting over to Rasp Pi
### Testing dependacies
Download and test if this will work:  
`conda install tensorflow-gpu scipy pyyaml python=3.6`  
`pip install opencv-python==3.4.5.20`  
`conda install tensorflow-gpu=1`  => Python code expects TF1.0

Run:  
`python image_demo.py --model 75 --image_dir ./images --output_dir ./output`

List Dependacies:
`conda env export > environment.yml`


Worries:
iam using TF with GPU.
