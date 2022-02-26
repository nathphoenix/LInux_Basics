https://medium.com/@habibridho/docker-as-deployment-tools-5a6de294a5ff

docker container run --publish 80:80 nginx
this download image nginx from docker hub, started a new container from that image and open port 80 on the host ip to run

docker container run --publish 80:80 --detach nginx
detach method tells docker to run in the background, and we get the unique container id of our container

we view list of running containers using :
docker container ls 

to stop a running container from the list fo containers: we take the first three numbers or characters from the containers we want to stop
docker container stop 890

to view al list of containers created so far :
docker container ls -a, the numbers of containers is proportional to number of containers created when container is runned

to create a new container

docker container run --publish 80:80 --detach --name phoenix nginx

To view logs
docker container logs phoenix

docker container top : helps us get info about a running container

To remove a container: then put the first three characters of the container or all the letters
docker container rm 734

to force remove a running container
docker container rm -f 734

Example on running mysql database server on docker:
docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
docker container run -d --name webserver -p 8080:80 httpd
the flag -p expose the port on you local machine

to check if it is running without using the browser:
curl localhost or curl localhost:8080

Getting inside a container
docker container run -it --name proxy nginx bash 
bash is one of the commandline interafce found in a container that gives you a shell to work with
the i stand for interractivity

instaed of running a nginx, we want to run a linux distribution called ubuntu
docker container run -it --name ubuntu ubuntu     this install lighter version of ubuntu

this restart the ubuntu 
docker container start -ai ubuntu

to check what is running inside an already running container, we use the:
docker container exec

docker container exec -it mysql bash

docker container stats

docker container run -it alpine bash
this will throw an error as alpine is just 5mb in size, so the only command available insisde is 'sh'
we run this:
docker container run -it alpine sh to access the alpine on terminal,
once inside, we can then use apk to install the bash command line

to get the port of a running container, we run :
docker container port webhost

HOW TO VIEW NGINX LOG
for example, container-name = nginx-standard
sudo docker logs -f container-name 1>/dev/null

HOW TO VIEW NGINX ACCESS LOG 
sudo docker logs -f nginx-standard 2>/dev/null


HOW TO PUSH YOUR IMAGE TO DOCKER HUB
docker commit d82ba8234ad2 nathphoenix/flask_standard_movie_app
d82ba8234ad2 = id of the docker container
flask_standard_movie_app = the name of the container

HOW TO DELETE OR REMOVE A CONTAINER
Docker rm
docker rm removes containers by their name or ID.

When you have Docker containers running, you first need to stop them before deleting them.

Stop all running containers: docker stop $(docker ps -a -q)
Delete all stopped containers: docker rm $(docker ps -a -q)

REMOVE ALL DIRECTORIES IMAGES ON DOCKER
docker system prune -a

AFTER STARTING MINIKUBE DO THIS

1. minikube -p minikube docker-env

2. point our terminal to docker environment : eval $(minikube -p minikube docker-env)

Once you're done building you can unset docker env i.e. disconnect your minikube env by unsetting these docker configs if you run 

minikube docker-env --unset


PROBLEMS
one thing to remember regarding 'minikube' is that minikube's host is not the same as your local host, therefore, 
what i realized, that in order to use local images for testing with minikube you must build your docker image first 
locally or pull it locally and then add it using the command bellow into the minikube context which is, nothing else as another linux instance.

minikube image rm image <image>:<tag>
minikube load image <image>:<tag> --daemon


TO GET THE DETAILS OF A KUBERNETES SERVICE
kubectl describe service hello-python-service

HOW TO RUNA DOCKER FILE WITHOUT DOCKER COMPOSE
docker build -t <image_name> .


STARTING YOUR KUBERNETES APP
1. kubectl
2. minikube start
3. minikube -p minikube docker-env
4. minikube -p minikube docker-env | Invoke-Expression
5. after configuring yaml file, do this to run the app :  kubectl apply -f deployment.yaml
6. then start the service with :  minikube service flask-standard-service







