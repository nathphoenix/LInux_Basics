sudo apt update
sudo apt-get upgrade

at this point python3 is already installed
sudo apt-get install python3-pip libpq-dev

if not install
sudo apt-get install python3-pip python3-dev libpq-dev

sudo apt install virtualenv
virtualenv venv --python=python3

source venv/bin/activate

install desired version of tensorflow
pip3 install https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.14.0-py3-none-any.whl