# Aims
* Figure how use PoseNet Python Implementation
* Run Python Implementation on My Computer
* Run Python Implementation on rasp pi
* Port over into container + ARM32

TODO:  
First -> Test inferencing speed on images:
* Test if conda envrionment works -> works
* Port over to Rasp Pi, see if conda + everything works there. -> modifications to libraries
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
`python3 image_demo.py --model 75 --image_dir ./images --output_dir ./output`

List Dependacies:
`conda env export > environment.yml`


Worries:
iam using TF with GPU.

### Commands Ran On Rasp Pi
```
git clone https://github.com/16fb/posenet-python.git
python3 get_test_images.py

### Installing MiniConda On Rasp Pi [Guide](https://stackoverflow.com/questions/39371772/how-to-install-anaconda-on-raspberry-pi-3-model-b)
wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-armv7l.sh
sudo md5sum Miniconda3-latest-Linux-armv7l.sh
sudo /bin/bash Miniconda3-latest-Linux-armv7l.sh

conda config --add channels rpi

#conda install python=3.5
#conda install python=3.6


### Dependacies
conda create --name PoseNet python=3.6
source activate PoseNet
pip3 install tensorflow
pip3 install opencv-python
conda install scipy pyyaml 

### bunch of missing dependacies i dunno if i must have
pip3 install opencv-contrib-python; sudo apt-get install -y libatlas-base-dev libhdf5-dev libhdf5-serial-dev libatlas-base-dev libjasper-dev  libqtgui4  libqt4-test


### welp reinstall python [theres python 3.4 in my system for some god forsaken reason] (its anaconda base python version)
sudo apt remove python3-dev python3-pip python3-venv
sudo apt install python3-dev python3-pip python3-venv
sudo apt remove python3
sudo apt install python3
sudo apt remove python
sudo apt install python
sudo su
conda update python


### Maybe?
sudo apt-get install libatlas-base-dev


python3 image_demo.py --model 75 --image_dir ./images --output_dir ./output
```

### Nani
Python 3.6 [Anaconda], has conda stuff, but no tensorflow
Python 3.7 [Comes with rasp pi], no conda stuff, got tensorflow

### Target
Python 3.7, with TF and other libraries.
using pip3, 
anaconda/berry conda cannot find libraries for python 3.7, and for reason cannot find tensorflow for armv7l

### New Code 
pip3 install tensorflow
pip3 install opencv-python
pip3 install numpy, scipy
pip3 install PyYAML
sudo apt-get install libatlas-base-dev
pip3 install opencv-contrib-python; sudo apt-get install -y libatlas-base-dev libhdf5-dev libhdf5-serial-dev libatlas-base-dev libjasper-dev  libqtgui4  libqt4-test

python3 image_demo.py --model 75 --image_dir ./images --output_dir ./output
