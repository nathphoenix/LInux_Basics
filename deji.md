    --Creating another user to give a non super user login options
        adduser nathphoenix                 # creates a user by name nathphoenix
    --making the user nathphoenix gain temporary access to being root, in order to be able to install packages e.t.c 
        visudo
            --navigate to "user priviledge specification"
            --Enter "nathphoenix ALL=(ALL: ALL) ALL" under "root ALL=(ALL: ALL) ALL"
            --press "Cntr O" to save on top of the existing file
            --press Enter button
            --press "Cntr X" to exit
    --setting user nathphoenix to be able to login directly just the same as root user
        vi /etc/ssh/sshd_config
            --navigate to  Authentication:
            --set "PermitRootLogin No" by pressing the "i" key to take us to insert mode while we set the default yes to no 
                --this is done to not allow other user compromise our server by being able to login
            --press escape key to leave the insert mode
            --navigate to  "PasswordAuthentication yes"
                pressing the "i" key to take us to insert mode
            --below "PasswordAuthentication yes" put "AllowUsers nathphoenix"
                This tells ssh which is connection protocol to allow user nathphoenix to connect to the server because we denied root user login 
                access for security reasons
            --press ESC key to leave the insert mode
            --press ":wq" to save the file, write to the disk and quit
            --"service sshd reload"         this reloads the service and allows us to use the save configuration
            --enter "exit" to disconnect from the server and let us login with user nathphoenix 
            --enter "ssh nathphoenix@droplets_IP_address" == "ssh nathphoenix@157.245.131.154"
            --enter a very strong password for user nathphoenix
                since this user has access to login as root, use the command below
            --sudo su
                then enter password again, and this log us in as root user after which we can update packages with "apt-get update" if we like
            --exit
                takes us back to user nathphoenix
            --logout



       --setting up nginx and our rest API
        installing nginx and running our app, nginx will act as a gateway between our app and external users,nginx is called the reverse proxy
        nginx will communicate with uwsgi to enable a multithreaded operation of our flask app
        nginx can allow us run multiple flask app simultaneously in our server while redirecting incoming request to different apps 
        depending on some parameters
        --ssh nathphoenix@157.245.131.154               # login to the server
        --sudo apt-get update
        --sudo apt-get install nginx
        --sudo ufw status                       # ufw == ubuntu firewall
            letting nginx have access through our firewall so that the incoming request don't get blocked
        --sudo ufw enable
        --sudo ufw allow 'Nginx HTTP'
            giving nginx access by putting Nginx in the firewall
        --sudo ufw status
            reveals the new status 
        --sudo ufw allow ssh
            prevents us from being locked out of the server
        --systemctl status nginx
            checks if nqinx is running
        --systemctl stop nginx
            stops nginx if it is running
        --sudo systemctl start nginx
            starts nginx if it is not running
        --sudo systemctl restart nginx
            restarts nginx if it is running             close the connection to our computer



        --sudo vi /etc/nginx/sites-available/images-rest.conf


        server {
            listen 80;
            real_ip_header X-Forwarded-For;
            set_real_ip_from 127.0.0.1;
            server_name localhost;
            location / {
                include uwsgi_params;
                uwsgi_pass unix:/var/www/html/images-rest/socket.sock;
                uwsgi_modifier1 30;
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



        --sudo nginx -t   to test the configuration file we created
        --ESC
        --:wq
        --sudo ln -s /etc/nginx/sites-available/images-rest.conf /etc/nginx/sites-enabled/


        --sudo mkdir /var/www/html/images-rest

        --sudo chown nathphoenix:nathphoenix /var/www/html/images-rest

        --cd cd /home/images-rest
            going into the directory
        -- cp -r . /home/images-rest   to copy all our files to our   desired directory to run our app

         --git clone https://github.com/nathphoenix/image_scraper.git .
        --mkdir log
        --sudo apt-get install python-pip python3-dev libpq-dev
        --pip install virtualenv
        --virtualenv venv --python=python3.6
        --source venv/bin/activate
        --& c:/Users/DELL/Desktop/hashtags/venv/Scripts/Activate.ps1
        --pip install -r requirements.txt


        This two works fine
        sudo apt install python3-virtualenv
        virtualenv venv --python=python3


        --sudo vi /etc/systemd/system/uwsgi_images_rest.service
            this command above is creating a text file
            --uwsgi_allyshop_rest.service cotents
                [Unit]  
                Description=uWSGI images-rest rest

                [Service] 
                Environment=DATABASE_URL=postgres://images-rest:Abraham1990#@localhost:5432/images-rest
                ExecStart=/var/www/html/images-rest/venv/bin/uwsgi --master --emperor /var/www/html/images-rest/uwsgi.ini --die-on-term --uid images-rest --gid images-rest --logto /var/www/html/images-rest/log/emperor.log
                Restart=always
                KillSignal=SIGQUIT
                Type=notify
                NotifyAccess=all

                [Install] 
                WantedBy=multi-user.target



       --ESC
        --:wq
        --vi uwsgi.ini
            Delete everything inside this file using "D + Shift + G" key
            uwsgi.ini contains 
                [uwsgi] 
                base = /var/www/html/images-rest
                app = run 
                module = %(app)

                home = %(base)/venv
                pythonpath = %(base)

                socket = %(base)/socket.sock

                chmod-socket = 777

                processes = 8

                threads = 8

                harakiri = 15

                callable = app

                logto = /var/www/html/images-rest/log/%n.log
        --ESC
        --:wq
        --sudo systemctl start uwsgi_allyshop_rest



        --sudo systemctl reload nginx
        --sudo systemctl restart nginx
        --sudo systemctl start uwsgi_allyshop_rest


Test nginx conf
    sudo nginx -c /etc/nginx/nginx.conf -t

Adding public key
    --ssh-keygen
    --cat ~/.ssh/id_rsa.pub
    --cd ~/.ssh/id_rsa.pub


sudo systemctl stop nginx && sudo systemctl stop videoengine
> log/uwsgi.log
vi log/uwsgi.log
sudo systemctl start nginx && sudo systemctl start videoengine && sudo systemctl enable videoengine && sudo systemctl status videoengine

vi log/uwsgi.log
vi log/emperor.log
vi var/log/nginx/access.log
vi var/log/nginx/error.log
