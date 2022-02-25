SUMMARY IN STEPS

STARTING YOUR KUBERNETES APP
1. kubectl
2. minikube start
3. minikube -p minikube docker-env
4. minikube -p minikube docker-env | Invoke-Expression
5. after configuring yaml file, do this to run the app :  kubectl apply -f deployment.yaml
6. then start the service with :  minikube service flask-standard-service


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

