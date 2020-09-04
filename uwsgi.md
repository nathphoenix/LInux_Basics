unit is a section of the service that allows us to define some properties of the service, one of the service we are going to define within this unit section is the description of the service, this is going to say we are running the service that we are describing

[Unit]
Descrition=UWSGI items 

[Service]                                                                this is the database we are access
Environment=DATABASE_URL=postgres://nathphoenix:church89@localhost:5432/nathphoenix

this is what programs the service runs, this tells ubuntu that this is a service that can be started when the computer or server start, we then tell it the program we want to runwhich is the UWSGI, the mster below tells it to use a master process, which is what UWSGI use to keeps track of other processes in case we have more than one, so it can restart them if they crash, --emperor is a controller, --die-on-term helps to kill the service when we indicate and the python code

ExecStart=/var/www/html/items-rest/venv/bin/uwsgi --master --emperor /var/www/html/items-rest/uwsgi.ini --die-on-term --uid nathphoenix --gid nathphoenix --logto /var/www/html/items-rest/log/emperor.log

Restart=always    this helps to estart incase of crashes or stop, then ubuntun will restart

KillSignal=SIGQUIT
Type=notify
NotifyAccess=all

[install]
WantedBy=multi-user.target




[Unit]
Description=UWSGI items rest

[Service]
Environment=DATABASE_URL=postgres://nathphoenix:church89@localhost:5432/nathphoenix

ExecStart=/home/images-rest/venv/bin/uwsgi --master --emperor /home/images-rest/uwsgi.ini --die-on-term --uid nathphoenix --gid nathphoenix --logto /home/images-rest/log/emperor.log

Restart=always

KillSignal=SIGQUIT
Type=notify
NotifyAccess=all

[install]
WantedBy=multi-user.target

Ukeme part

[Unit]  
Description=uWSGI Article Video Engine story rest
After=network.target
[Service] 
WorkingDirectory=/home/ukeme
Environment="PATH=/home/ukeme/venv/bin"
Environment="MONGO_URL=mongodb://Bloverse:uaQTRSp6d9czpcCg@64.227.12.212:27017/social_profiling?authSource=admin&readPreference=primary&appname=MongoDB%20Compass&ssl=false"
Environment="base_dir=/home/ukeme"
ExecStart=/home/ukeme/venv/bin/uwsgi --master --emperor /home/ukeme/uwsgi.ini --die-on-term --uid ukeme --gid ukeme --logto /home/ukeme/log/emperor.log
Restart=always
KillSignal=SIGQUIT
Type=notify
NotifyAccess=all
[Install] 
WantedBy=multi-user.target