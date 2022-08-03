SUMMARY IN STEPS

STARTING YOUR KUBERNETES APP

0. Use powershell admin mode!! not tested with regular powershell
0a. Build your docker image if not available with "docker-compose build" or "docker build -t flask-kubernetes ." if docker-compose.yml file is not use or available.
1. kubectl
2. minikube start
3. minikube -p minikube docker-env    #to access docker vm, this command reconfigure our docker cli temporarily for the actual terminal
4. minikube -p minikube docker-env | Invoke-Expression
5. Enable addons :  minikube addons enable metallb # This step can be ignore at first unless there is an issue with endpoint availability
6. after configuring yaml file, do this to run the app :  kubectl apply -f deployment.yaml
7. Load local image minikube image load ContainerName(from the deployment.yaml) i.e minikube image load flask-standard_movie_app or  minikube cache add flask-standard_movie_app:latest
8. Verify that there are pods running using : kubectl get pods
9. then start the service with :  minikube service flask-standard-service or minikube service flask-standard-service --url
Then on another terminal,
minikube tunnel
10. check the dashboard : minikube dashboard

11. access your app on http://localhost:9900 or http://127.0.0.1:9900/

View the pod and services
kubectl get pod,svc -n kube-system

View the logs of a docker container
docker logs container_id

kubectl logs pod_name

How to execute and access a pod
kubectl exec -it pod_name sh

get details of pod
kubectl get pod -o wide

get deployments details
kubectl get deployment flask-standard -o yaml

To get the ip address to access our app externally
minikube ip

download deployment details
kubectl get deployment flask-standard -o yaml > deployment_result.yaml

Get the endpoint
kubectl get endpoints flask-standard-service

Cleanup the deployment and service using the following command
kubectl delete -f deployment.yaml

Stop services

minikube stop
minikube delete --all --purge

Execute minikube
minikube ssh

port forwarding
kubectl port-forward service/flask-standard-service 9800:9900

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

