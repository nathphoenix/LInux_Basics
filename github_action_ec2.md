After adding all the environment variables to the github repo,

ssh -i "phoenix.pem" ubuntu@ec2-34-234-85-39.compute-1.amazonaws.com

key : the content of the phoenix.pem file
username : mostly ubuntu(for aws only, others will be different)
host: ec2-34-234-85-39.compute-1.amazonaws.com


Then login to the ec2 server and install docker on it(steps in dockeer-deploy-aws.md, the file is here)
then clone the github repo into the the server either by using the github action file or manually on the server.

After the above is successful, then go to security group and port 80 to the inbound traffic, image guideline is gihub.jpg
