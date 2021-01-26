# Aim
Debian buster for ARMv7l, installing everything using pip


asn1crypto    0.24.0
cryptography  2.6.1
entrypoints   0.3
keyring       17.1.1
keyrings.alt  3.1.1
pip           18.1
pycrypto      2.6.1
PyGObject     3.30.4
pyxdg         0.25
SecretStorage 2.3.1
setuptools    40.8.0
six           1.12.0
wheel         0.32.3

### PLANS
maybe use a debian installation, and try get requirements.txt to work


* Unable to find tensorflow???
https://linuxize.com/post/how-to-install-tensorflow-on-debian-10/



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

### Idea:
run new container
download and install tensorflow
download and install openc-contrib python
download the rest from requirements.txt


### Later Idea
IDEA:: Use a rasbian buster container instead
- doubt too much speed lost
- easier to reconstruct on rasp pi.

