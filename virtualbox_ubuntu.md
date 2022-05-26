For software installation issue on ubuntu
sudo gnome-software
https://askubuntu.com/questions/1029382/i-do-not-have-permission-to-install-new-software

expand ubuntu view from small to big
sudo apt install build-essential dkms linux-headers-$(uname -r)

sudo apt update
sudo apt-get upgrade

at this point python3 is already installed
sudo apt-get install python3-pip libpq-dev

if not install
sudo apt-get install python3-pip python3.6-dev libpq-dev

for python2 setup
sudo apt-get install python-pip python-dev libpq-dev

sudo apt install virtualenv
virtualenv venv --python=python3
OR
virtualenv venv --python=python      For python2

source venv/bin/activate

install desired version of tensorflow
pip3 install https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.0.0-py3-none-any.whl

then uninstall in case of error
pip uninstall tensorflow

Now install back with the regular approach
pip uninstall tensorflow==1.0.0


sudo apt-get pkg-config




pip freeze > requirements.txt