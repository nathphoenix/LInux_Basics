from asyncore import file_dispatcher
from sre_constants import BRANCH


Push code to github as master BRANCH

Login to travis

Then link the above project to travis

create a travis configuration file and write your test to see if it works fine 

Login to aws to create Elastic beanstalk app

We then click on create and environment after entering the application name and other details
Creating takes some minutes, then we move to our project and edit our travis file by adding our deployment configuration

deployment configuration can be gotten from the AWS EBS page
we get the name of the app
we get the region of the EBS server
we get the s3 name which is automatically generated when the EBS application was created on AWS, we then go into the search menu and type 'S3' then we see the s3 that was created, click it and get the name which looks like this 'elasticbeanstalk-us-east-1-960726601836'

After completing the above configuration settings in the travis file, we then move to AWS platform and setup IAM configuration.

type in search bar for the IAM settings
create a new user and then click on group policy, type beanstalk in the search bar and tick 'Provide full access to aws beanstalk' OR ADMIN ACCESS, the click next and create user

Make sure to download the csv generated in case you forget secret access key

Then we head to travis website and store our generated credentials, you can check the images folder here called EBS-AWS

After storing the credentials we then add the variable name to our travis file

Then we commit and push all changes to the repo.


IMPORTANT NOTICE!!!!

IF after the push, this error ocurred 'Aws::S3::Errors::SignatureDoesNotMatch',
Generate another credentials under the same user, as you can see(IAM IMAGE), we have two crdentials here, which is bcos one of them failed 

IF you get health check error in red color i.e 'ELB health is failing or not available for all instances.'
This is bcos, ELB is automatically map to port 80, so you have to set your EXPOSE port in dockerfile and docker-compose accordingly to 80 instead of other ports that was use, i change it from 9900 to 80.

Another option is to include your PORT on ELB just like we normally do on EC2 instance, this can be done in the following way