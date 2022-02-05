https://stackoverflow.com/questions/55860101/how-do-i-run-a-cronjob-with-a-python-virtual-environment

Ctrl+D to kill a .sh file 


METHOD 1 creating a .h file and put your command 
#!/bin/bash
source /home/nathphoenix/Project/venv/bin/activate
python /home/nathphoenix/Project/rss.py >> /home/nathphoenix/Project/cron.log 2>&1


https://stackoverflow.com/questions/55860101/how-do-i-run-a-cronjob-with-a-python-virtual-environment

Method 2

1. Lunch crontab -e
2. */5 * * * * source /home/nathphoenix/Project/venv/bin/activate python /home/nathphoenix/Project/rss.py >> /home/nathphoenix/Project/cron.log 2>&1


To handle permission issue
chmod u+x /home/nathphoenix/Project/report.log



Final working method:
It runs every 1 minutes
*/1 * * * * /home/nathphoenix/Project/venv/bin/activate && python /home/nathphoenix/Project/test.py >> /home/nathphoenix/Project/cron.log 2>&1

*/1 * * * * /home/nathphoenix/Documents/Project/venv/bin/activate && python /home/nathphoenix/Project/test.py >> /home/nathphoenix/Project/cron.log 2>&1

Full step

after creating your droplet

sudo apt upgrade

To change to python3 version
https://stackoverflow.com/questions/41986507/unable-to-set-default-python-version-to-python3-in-ubuntu
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
