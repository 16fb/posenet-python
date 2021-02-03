# Aim
Debian buster for ARMv7l, installing everything using pip


# Whats Going On + Plans
AIM:: Get PoseNet to work on docker container (debian/armv7l)

I have tmux window running debian docker container as root on rasp pi.
i gonna try install apt for stuff, and pip3 pull for stuff.


### Current Problem
Tensorflow not installed 
[Main unofficial repo link](https://github.com/lhelontra/tensorflow-on-arm/releases)
[Download Link](https://github.com/lhelontra/tensorflow-on-arm/releases/download/v1.14.0-buster/tensorflow-1.14.0-cp37-none-linux_armv7l.whl)

apt install -y wget
wget https://github.com/lhelontra/tensorflow-on-arm/releases/download/v1.14.0-buster/tensorflow-1.14.0-cp37-none-linux_armv7l.whl
pip3 install tensorflow-1.14.0-cp37-none-linux_armv7l.whl

pip3 install -r ./Docker/requirements.txt

Problem:
Building h5py requires pkg-config unless the HDF5 path is explicitly specified

apt install libhdf5-dev python-dev pkg-config
pip3 install h5py

Problem:
seems to be installing opencv-python incorrectly.

apt install build-essential cmake pkg-config
apt install libjpeg-dev libtiff5-dev libjasper-dev libpng-dev
apt install libxvidcore-dev libx264-dev
apt install libatlas-base-dev gfortran
apt install libhdf5-dev libhdf5-serial-dev libhdf5-103
apt install libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5
apt install python3-dev

apt install libffi6 libffi-dev 
apt install libssl-dev

pip3 install --upgrade pip

pip3 install pyOpenSSL
pip3 install opencv-contrib-python

#pip3 install opencv-python

pip3 install scipy

## Idea the requirements.txt is fucked, need fix
Iam using different opencv [opencv-python -> opencv-contrib-python]\
different openCV as well, different from pip.


### Save current image
`docker commit <containerID> <ResultantImageName>`
`docker commit e6aa232e27dc 16fb/posenet:v1`


### docker save 
docker save --output posenet 16fb/posenet:v1

### remove dangling
docker container prune -f
docker image prune -f
docker volume prune -f
docker system prune

Sometimes you just need restart machine

### Idea:
run new container
download and install tensorflow
download and install openc-contrib python
download the rest from requirements.txt

`docker build -t 16fb/posenet:proper .`


## Running container in Atlas
Follow documentation page on connecting to Atlas

`docker load -i posenet`

`docker run -it 16fb/posenet:v1`

`python3 image_demo.py --model 75 --image_dir ./images --output_dir ./output`

AVG FPS: -> 1.16

`docker run --device=/dev/davinci_manager --device=/dev/hisi_hdc --device=/dev/davinci0 -it 16fb/posenet:v1`

`python3 image_demo.py --model 75 --image_dir ./images --output_dir ./output`

AVG FPS -> 1.39

`python3 benchmark.py --model 75`

### Notes
AI Core not being utilised ->
Main CPU Core being utilised ->

NEED CONVERT TF MODEL TO PROPRIETARY FILE.


## Running container in Rasp Pi
`docker run -it 16fb/posenet:v1`
`python3 image_demo.py --model 75 --image_dir ./images --output_dir ./output`

AVG FPS -> 0.83