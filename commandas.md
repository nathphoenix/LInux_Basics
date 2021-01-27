after creating droplet,

open gitbash and type
ssh root@161.35.97.66, the enter your password

you can then update packages as a root user
apt-get update

we add a user with this
adduser nathphoenix
then create password for the user immedately

we give the new user admin privileges using
usermod -aG sudo nathphoenix  (nathphoenix is the name of the user added)

We create ssh key by loging out of the server
ssh-keygen -t rsa -b 4096
and then copy this path to create the file
C:\Users\maxwell/.ssh/id_rsa
note you can change this "id_rsa" to your preferred name like "bloverse_gcp" or "nath_tb"
then press enter twice so that you will not use password to login using the public key generated



Next we send a public key to our cloud server on that bash terminal:

ssh-copy-id nathphoenix@161.35.97.66 using gitbash only (This doesn't seem to work again)
OR
cd into .ssh, then
ssh-copy-id -i phoenix_tb nathphoenix@157.245.243.176
ssh-copy-id -i Nathaniel nathphoenix@157.245.243.176
 



Then launch your instance
ssh nathphoenix@161.35.61.63
ssh nathphoenix@161.35.48.64 -i nathan


to stop logging in with password
sudo vim /etc/ssh/sshd_config
we then change PasswordAuthentication to no, on line 56 of the open file
press i to edit and esc to save. the :wq to save changes and enter

Then restart server with

sudo shutdown -r now


as a defined user, you upgrade your packages using the root permission
sudo apt upgrade

scp -i nathan -r image_scraper nathphoenix@167.172.141.50:~/Project


We can continue withis step below

logging in to a remote server from window
ssh nathphoenix@161.35.97.66 -i nathan

METHOD 1
This two works fine
sudo apt install python3-virtualenv
virtualenv venv --python=python3



We can setup virtualenv on vm :
sudo apt install python3-pip
pip3 install virtualenv
sudo apt install python3-pip
sudo apt install virtualenv

activate with
source .speech/bin/activate
https://dev.to/serhatteker/how-to-install-virtualenv-on-ubuntu-18-04-2jdi

if after this step, you have virtualenv error, 
do, pip uninstall virtualenv twice and try:  virtualenv flask --python=python3

or reinstall virtualenv

METHOD 2
We can setup virtualenv on vm
sudo apt-get install python-pip python3-dev libpq-dev
sudo apt install virtualenv
virtualenv flask --python=python3


RUNNING YOUR CODE IN BACKGROUND OR TRAINING
https://medium.com/codebase/how-to-keep-multiple-linux-terminals-running-in-background-screen-ccf2e53b0d22

how to transfer folder from local to remote server
scp -i nath_tb -r rss_scraper nathphoenix@157.245.243.176:~/Project

how to download folder from remote to local
scp -i nathan -r nathphoenix@161.35.97.66:~/Project/wavenet_vocoder .
scp -i phoenix_tb -r  videoengine@206.189.29.53:~/home/videoengine .

How to download all files from remote to local
if the project is not in any directory, use this
scp -i phoenix_tb -r  videoengine@206.189.29.53: .

how to transfer a single file from local to remote
scp -i bloverse-gcp news.pdf otseobande@34.73.28.53:~/Project
scp -i phoenix_tb -r rss_updated.py nathphoenix@157.245.243.176:~/Project
scp -i phoenix_tb -r blogger2.py medium@167.99.194.52:~/medium

for selecting multiple single file
 scp -i phoenix_tb -r algo_category.csv category_funcs.py nathphoenix@157.245.243.176:~/Project


how to download a single file from remote to local
scp -i nathan nathphoenix@157.245.84.132:~/Project/tacotron_model.ckpt-22500.meta .

when it is not in a folder
scp -i phoenix_tb medium@167.99.194.52:uwsgi.log .



how to extact tar.gz file
tar -xvzf ukulele_songs.tar.gz -C ~/Documents/Songs/

how to extracted tar.bz file
tar -xvjf LJSpeech-1.1.tar.bz2 -C ~/Project/tacotrons/


https:/cd /medium.com/dev-blogs/transferring-files-between-remote-server-and-local-system-133d78d58137





whoami
user1
$ su - user2
Password:
$ whoami
user2
$ exit
logout