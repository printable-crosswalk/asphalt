# asphalt
## Setup
- [Install docker](https://store.docker.com/editions/community/docker-ce-desktop-mac)

## Basic concepts
EC2 Container Service (ECS) has a 'task definition.' This takes in a built docker image. A docker image is built from a Dockerfile, which specifies how to set up and launch a container. A bunch of containers are grouped into a container cluster.

We're using Elastic Container Registry (ECR) to hold our built docker images.

## Starting the hello world application locally
- Build the docker image from the docker file. This will take a while.
	- `docker build -t hello-world .`
- Verify that the image built correctly.
	- `docker images --filter reference=hello-world`
- Run the docker image
	- `docker run -p 80:80 hello-world`

## Making a new ECR repository
- Create the repository
	- `aws ecr --profile=personal create-repository --repository-name hello-world`
- Tag the docker image with the repositoryUri returned from the previous step
	- `docker tag hello-world 748749006604.dkr.ecr.us-west-2.amazonaws.com/hello-world`
- Get the login string for the docker registry
	- `aws ecr --profile=personal get-login --no-include-email`
- Login by executing the login string from the previous step. This will authenticate you for 24 hours.
- Push the docker image to the repositoryUri from above
	- `docker push 748749006604.dkr.ecr.us-west-2.amazonaws.com/hello-world`
## Useful documentation
- [ECS' docker basics](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html)
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
