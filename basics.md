Delete directory and a sub directory
rm -rf wavenet_vocoder
pwd to view entire directory

to go into root directory
cd /

how to copy a file, test is the file you want to copy, testcopy is the new name, in thesame directory
cp test testcopy

if you wnt to copy into another folder
cp tacotron_model.ckpt-22500.data-00000-of-00001 /home/nathphoenix/Project

HOW TO COPY ALL FILES FROM ONE DIRECTORY TO ANOTHER
cp -r /items-rest/code/* .  (.) is to current directory
cp -r . /var/www/html/image-rest
cp -r ~/data/data/* .

HOW TO COPY A FILE TO ANOTHER DIRECTORY
cp -r /items-rest/code/ /home/nathphoenix/Project   to another directory
cp -r /items-rest/code/ /home/nathphoenix/Project

to delete text in vi text editor
D + shift +G

HOW TO CLEAR LOG FILES IN SERVER
you cd into the directory where you have your log file, in this case we have uwsgi.log
   > uwsgi.log

DELETE ALL FILES WITH A PARTICULAR EXTENSION

find . -type f -iname \*.jpg -delete
find . -type f -iname \*.txt -delete

HOW TO CREATE A FILE
cat > file.txt

how to make a file executable
 chmod -R 777 ~/Project/video_engine.csv

chmod u=rx file        (Give the owner rx permissions, not w)
chmod go-rwx file      (Deny rwx permission for group, others)
chmod g+w file         (Give write permission to the group)
chmod a+x file1 file2  (Give execute permission to everybody)
chmod g+rx,o+x file    (OK to combine like this with a comma)

chmod g+w blog.txt


#!/bin/bash
source /home/nathphoenix/Project/venv/bin/activate
python3 /home/nathphoenix/Project/video-rss.py  >> /home/nathphoenix/Project/cron.log 2>&1


another method to create a file
touch docker-compose.yml


HOW TO CREATE VIRTUALENV ON WINDOWS
virtualenv Cryptovenv --python=python