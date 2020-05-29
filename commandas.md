after creating droplet,

we add a user with this
adduser nathphoenix

we give the new user admin privileges using
usermod -aG sudo nathphoenix  (nathphoenix is the name of the user added)

We create ssh key by loging out of thw server
 ssh-keygen -t rsa -b 4096
and then copy this path to create the file
C:\Users\Maxwell/.ssh/id_rsa

Next we send a public key to our cloud server
ssh-copy-id nathphoenix@161.35.96.50 using gitbash only

to stop logging in with password
sudo vim/etc/ssh/sshd_config
we then change PasswordAuthentication to no, on line 56 of the open file
press i to edit and esc to save. the :wq to save changes and enter

Then restart server with
sudo service ssh restart

scp -i nath-gcp -r Tacotron-2 nathphoenix@161.35.96.50:~/Project


We can continue withis step below

logging in to a remote server from window
ssh otseobande@34.73.28.53 -i bloverse-gcp

We can setup virtualenv on vm :
pip3 install virtualenv
sudo apt install virtualenv
https://dev.to/serhatteker/how-to-install-virtualenv-on-ubuntu-18-04-2jdi

RUNNING YOUR CODE IN BACKGROUND OR TRAINING
https://medium.com/codebase/how-to-keep-multiple-linux-terminals-running-in-background-screen-ccf2e53b0d22

how to transfer folder from local to remote server
scp -i bloverse-gcp -r tacotron otseobande@34.73.28.53:~/Project

how to transfer a single file
scp -i bloverse-gcp news.pdf otseobande@34.73.28.53:~/Project

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