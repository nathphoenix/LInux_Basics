https://www.youtube.com/watch?v=L_1qbt-Iii0

What is Cloud Deploy
. Cloud Deploy is a managed service that automates delivery of your applications
to a series of target environments in a defined promotion sequence.

. When you want to deploy your updated application, you create a release,
whose lifecycle is managed by a delivery pipeline.

· Cloud Deploy uses Scaffold for rendering, deployment, and
Skaffold, you can also easily connect your local developme
Derloy continuous delivery pipeline.

First create your kubernetes cluster


grant all IAM perermission
https://cloud.google.com/iam/docs/creating-custom-roles

Then type build trigger and create a cloud build trigger to link your repo to the build trigger by selecting triggers and create a new one

create your container registry repository (artifact) for saving docker image
#create gke-repo(Artifact registry) with https://console.cloud.google.com/artifacts/create-repo?project=kubernetes-cloud-432317
  # images:
  # - 'us-central1-docker.pkg.dev/<your_project_id>/gke-repo/quickstart-image'

and then create your kubernetes YAML with the deployment and service configuration like a regular kubernetes cluster on local.

A delivery pipeline is a representation of the workflow that delivers an application to each target in a deployment progression.

Then cloudbuil.yml file and 
Then scalfolding.yml

check the gke-cicd project 