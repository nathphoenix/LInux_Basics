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
C:\Users\Nathaniel/.ssh/id_rsa
note you can change this "id_rsa" to your preferred name like "bloverse_gcp" or "nath_tb"
then press enter twice so that you will not use password to login using the public key generated



Next we send a public key to our cloud server on that bash terminal:

ssh-copy-id nathphoenix@161.35.97.66 using gitbash only (This doesn't seem to work again)
OR
cd into .ssh, then
ssh-copy-id -i nath_tb nathphoenix@167.172.141.50




Then launch your instance
ssh nathphoenix@161.35.61.63
ssh nathphoenix@157.245.243.176 -i nathan


sudo apt-get update

sudo apt-get install nginx

sudo ufw enable
sudo ufw allow ssh
systemctl start nginx
sudo systemctl start nginx
sudo systemctl status nginx
sudo nano /etc/nginx/sites-available/medium.conf

server {
    listen 80;
    real_ip_header X-Forwarded-For;
    set_real_ip_from 127.0.0.1;
    server_name localhost;
    location / {
        include uwsgi_params;
        uwsgi_pass unix:/home/medium/socket.sock;
        uwsgi_modifier1 30;
	uwsgi_read_timeout 300s;
	uwsgi_connect_timeout 300s;
	uwsgi_send_timeout 300s;
    }
    error_page 404 /404.html;
    location = /404.html {
        root /usr/share/nginx/html;
    }
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }
}

Anytime you edit your .conf file, you should always restart your nginx
systemctl restart nginx




sudo nginx -t
sudo ln -s /etc/nginx/sites-available/medium.conf /etc/nginx/sites-enabled/
sudo nginx -t
pwd
sudo mkdir /home/medium
sudo chown medium:medium /home/medium
cd /home/medium
mkdir log
sudo nano uwsgi.ini


[uwsgi]
base = /home/medium
# master = true
app = app
module = %(app)
home = %(base)/venv
pythonpath = %(base)
socket = %(base)/socket.sock
enable-threads = true
chmod-socket = 777
#http-timeout = 3600000
processes = 4
threads = 4
callable = app
logto = /home/medium/log/%n.log


ls
sudo apt-get install python-pip python3-dev libpq-dev
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev 
pip install virtualenv
virtualenv venv --python=python3.6
source venv/bin/activate

[Unit]
Description=uWSGI medium rest
[Service]
Environment="BASE_DIR=/home/medium
Environment="PATH=/home/medium/venv/bin"
Environment="APP_SECRET_KEY=ayodeji"
ExecStart=/home/medium/venv/bin/uwsgi --master --emperor /home/medium/uwsgi.ini --die-on-term --uid medi
um --gid medium --logto /home/medium/log/emperor.log
Restart=always
KillSignal=SIGQUIT
Type=notify
NotifyAccess=all
[Install]
WantedBy=multi-user.target


sudo systemctl restart medium.service