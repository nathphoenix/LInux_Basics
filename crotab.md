FOR UBUNTU WSL ON WINDOWS
Start the service manually first with
sudo cron start   (because the service is not running automatically)

WORKS IN 2022
METHOD 1 creating a .h file and put your command 
#!/bin/bash
source /home/nathphoenix/Project/venv/bin/activate
python /home/nathphoenix/Project/test_cron.py >> /home/nathphoenix/Project/cron.log 2>&1
then crontab -e
#*/1 * * * * bash /home/nathphoenix/Project/math.sh



https://stackoverflow.com/questions/55860101/how-do-i-run-a-cronjob-with-a-python-virtual-environment

Ctrl+D to kill a .sh file 

WORKS IN 2022
METHOD 1 creating a .h file and put your command 
#!/bin/bash
source /home/nathphoenix/Project/venv/bin/activate
python /home/nathphoenix/Project/test_cron.py >> /home/nathphoenix/Project/cron.log 2>&1
then crontab -e
#*/1 * * * * bash /home/nathphoenix/Project/math.sh


https://stackoverflow.com/questions/55860101/how-do-i-run-a-cronjob-with-a-python-virtual-environment

Method 2

1. Lunch crontab -e
2. */5 * * * * source /home/nathphoenix/Project/venv/bin/activate python /home/nathphoenix/Project/rss.py >> /home/nathphoenix/Project/cron.log 2>&1


To handle permission issue
chmod u+x /home/nathphoenix/Project/report.log



Final working method:
It runs every 1 minutes
*/1 * * * * /home/nathphoenix/Project/venv/bin/activate && python /home/nathphoenix/Project/test_cron.py >> /home/nathphoenix/Project/cron.log 2>&1

Final working method In 2022:

*/1 * * * * python /home/nathphoenix/Project/test_cron.py >> /home/nathphoenix/Project/cron.log 2>&1

It runs every 1 minutes
*/1 * * * * /home/nathphoenix/Project/venv/bin/activate python /home/nathphoenix/Project/test_cron.py >> /home/nathphoenix/Project/cron.log 2>&1

NOT WORKING
*/1 * * * * /home/nathphoenix/Documents/Project/venv/bin/activate && python /home/nathphoenix/Project/test.py >> /home/nathphoenix/Project/cron.log 2>&1

WORKS
*/1 * * * * python /home/nathphoenix/test_cron.py >> /home/nathphoenix/cron.log 2>&1

Full step

after creating your droplet

sudo apt upgrade

To change to python3 version
https://stackoverflow.com/questions/41986507/unable-to-set-default-python-version-to-python3-in-ubuntu
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10


