after creating server, before you create a user, we install the package we need as an admin
apt-get install postgresql
apt-get install postgresql-contrib or apt-get install postgresql postgresql-contrib

We login to postgres as a postgres user
sudo -i -u postgres

we then create a postgres user which should be the name of the unix user "nathphoenix" in the database. The P flag allows us to add password

createuser nathphoenix -P

we can create a db as an example
createdb commerce

then we exit "exit" twice out of postgres and root user

we connect to our database, every user in postgres automatically connect to a database, becasue as we are connecting the database is created automatically which is called "postgres"
psql

to get connection info 
\conninfo

to logout of the database
\q
we then type exit to go back to the root user

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
C:\Users\Maxwell/.ssh/id_rsa
note you can change this "id_rsa" to your preferred name like "bloverse_gcp" or "nath_tb"
then press enter twice so that you will not use password to login using the public key generated

Next we send a public key to our cloud server on that bash terminal
ssh-copy-id nathphoenix@161.35.97.66 using gitbash only

Then launch your instance
ssh nathphoenix@161.35.61.63 

           NEXT STAGE
become root user again from user nathphoenix
sudo su

We login to postgres as a postgres user
sudo -i -u postgres

we then create a postgres user which should be the name of the unix user "nathphoenix" in the database. The P flag allows us to add password

createuser nathphoenix -P

we can create a db as an example
createdb nathphoenix

then we exit "exit" twice out of postgres and root user

we then connect to the db psql

you can also drop database but must be database user
dropdb

then we secure our databse so that we login with our password anytime we connect to database as the database user. This is very important as sqlalchemy will not work if we don't do that

sudo vim /etc/postgresql/10/main/pg_hba.conf, we change loacal from peer to md5 by scrolling down the list
sudo vim /etc/postgresql/10/main/postgresql.conf, this direct us to the above file path, not necessary again
hba_file = /etc/postgresql/10/main/pg_hba.conf

https://linuxize.com/post/how-to-install-postgresql-on-ubuntu-18-04/

To quit a notepad in linux, use
:q!

To view list of all databse
\l+

to stop logging in with password
sudo vim /etc/ssh/sshd_config
we then change PasswordAuthentication to no, on line 56 of the open file
press i to edit and esc to save. the :wq to save changes and enter

Then restart server with

sudo shutdown -r now


as a defined user, you upgrade your packages using the root permission
sudo apt upgrade

WE THEN INSTALL
sudo apt-get install nginx

To prevent firewall issues
sudo ufw status        (ufw is ubuntu firewall)
if inacative then we enable with
sudo ufw enable

Then to allow,
sudo ufw allow 'Nginx HTTP'    This will now put Nginx in firewall
then check the status again
sudo ufw status

JUST A NOTE ON VISUDO
visudo   uses nano editor which opens the default permission file

Then we type this so we don't get locked out of the server
sudo ufw allow ssh

Then we check if Nginx is running with the system controller
systemctl status nginx,     we will be using this alot
 we can use systemctl to stop and start nginx
systemctl stop nginx
systemctl start nginx
systemctl restart nginx

systemctl reload nginx  is better than all

then we add api config to nginx config to make sure it can access our api

https://phoenixnap.com/kb/install-nginx-on-ubuntu
sudo vi /etc/nginx/sites-available/default  (This opens the default config file)

sudo vi /etc/nginx/sites-available/items-rest.conf  (This later work)

open the "nginx_api.config" in this tutorial folder and paste the code into the open file on the instance

we then enable the config file with the command below, what this will do is that it will link the config file to the site enabled folder where nginx read the config property
sudo ln /etc/nginx/sites-available/items-rest.conf /etc/nginx/sites-enabled/

we create our socket connections
First we create the folder where our config file lives
sudo mkdir /var/www/html/items-rest

A user of this instance will not have access to the folder because we use  sudo command to create the folder, to enable the user have access to the folder or change owner access of the folder

sudo chown -v -R nathphoenix:nathphoenix /var/www/html/items-rest
sudo chown nathphoenix:nathphoenix /var/www/html/items-rest

HOW TO COPY ALL FILES FROM ONE DIRECTORY TO ANOTHER
 cp -r /items-rest/code/* .

Then we cd into the directory 
cd /var/www/html/items-rest
we create our log file to monitor any issue
mkdir log

after that u can then clone your project into that direct either with git or anyother methods that you know

METHOD 2
We can setup virtualenv on vm
sudo apt-get install python-pip python3-dev libpq-dev
sudo apt install virtualenv
virtualenv flask --python=python3

SETTING UP USWGI TO RUN REST API
We will start with changing the uswgi.ini file, but first we will create a ubuntu service, aservice is what we can tell ubuntu to run, when the computer start and when the server start and you can tell it to restart it and crash.
Essentially a service is the descriptor of a programme and u can tell

sudo vi /etc/systemd/system/uwsgi_items_rest.service
after this we continue with the file called uwsgi.md and copy the code

Then we  edit the uwsgi.ini file in the project folder, check the uwsgi.ini here 

WE CAN START OUR FLASK APP NOW

sudo systemctl start uwsgi_items_rest

TO CHECK THE LOG FILE
vi log/uwsgi.log

TESTING OUR API
First we have to make sure we remove the default nginx config file
sudo rm /etc/nginx/sites-enabled/default

after that we reload our service
systemctl daemon-reload or sudo systemctl reload nginx
sudo systemctl restart nginx

Next
uwsgi will load our flask app with this command
sudo systemctl start uwsgi_items_rest

Then we go to our postman and make request and get request to test




THE END





we then login into postgres again

scp -i nathan -r Tacotron-2 nathphoenix@161.35.97.66:~/Project

scp -i nathan -r code nathphoenix@161.35.97.66:~/items-rest



We can continue withis step below

logging in to a remote server from window
ssh nathphoenix@161.35.97.66 -i nathan

We can setup virtualenv on vm :
pip3 install virtualenv
sudo apt install python3-pip
sudo apt install virtualenv
virtualenv .speech
virtualenv .speech --python=python3
activate with
source .speech/bin/activate
https://dev.to/serhatteker/how-to-install-virtualenv-on-ubuntu-18-04-2jdi

RUNNING YOUR CODE IN BACKGROUND OR TRAINING
https://medium.com/codebase/how-to-keep-multiple-linux-terminals-running-in-background-screen-ccf2e53b0d22

how to transfer folder from local to remote server
scp -i bloverse-gcp -r tacotron otseobande@34.73.28.53:~/Project

how to transfer from remote to local
scp -i nathan -r nathphoenix@161.35.97.66:~/Project/wavenet_vocoder .

how to transfer a single file
scp -i bloverse-gcp news.pdf otseobande@34.73.28.53:~/Project

how to extact tar.gz file
tar -xvzf ukulele_songs.tar.gz -C ~/Documents/Songs/

how to extracted tar.bz file
tar -xvjf LJSpeech-1.1.tar.bz2 -C ~/Project/tacotrons/


https:/cd /medium.com/dev-blogs/transferring-files-between-remote-server-and-local-system-133d78d58137
