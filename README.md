<h1>Important Concepts</h1>

**Container**: A container is lightweight way to package applications including all their dependencies and necessary files while keeping them isolated from other containers in the same system.

**Container image**: A _container_ is run from a _container image_. A container image is a static version of all the files, environment variables, and the default command/program that should be present in a container. Static here means that the container image is not running, it's not being executed, it's only the packaged files and metadata.

**Difference between container and container image**: A container refers to the running instance, the thing that is being executed. A container image refers to all the things needed to build a container instance.

<h1>Basic Commands</h1>

**docker --version**: Get the current version of Docker.<br>

**docker info**: General info about Docker.<br>

**docker pull**: Get the indicated image from the DockerHub.<br>

**docker run --name my_own_name image_name**: Build and run a container with the given name.<br>

**docker run image_name my_own_command**: Build and run the container, overrides the COMMAND of the image.<br>

**docker exec container_id my_command**: In a container that already exists and is running execute a command.<br>

**docker rename current_name new_name**: Change the name of the given container.<br>

**docker rm container_id**: Removes the given container. Instead of the container id we can also use the container name.<br>

**docker container prune**: Removes all the stoped containers.<br>

**docker system prune**<br>

**docker rm -f $(docker ps -aq)**: Removes all the containers (q returns all the ids of the containers).<br>

**docker run -it image_name**: Build and run the container in the interactive mode (for example when running Ubuntu).<br>

**docker images**: List all the images we have installed in our system. We can al use **docker image ls**<br>

**docker images | head**: Same as _docker images_ but only show a few lines.<br>

**docker run -d image_name**: (_-d_ is for detach), run the given container in the background.<br>

**docker run -d --rm -p 8000:80 --name my-name imageName**: Run the given container in the background with the name that we have set, the container is removed when we stop it, the -p maps the port 80 of the Docker container to our port 8000.

**docker logs containerId**: Show the logs of the given container at the current moment and then return the control.<br>

**docker logs -f containerId** Same as _docker logs_ but stays listening.<br>

**docker top containerName** Displays the running processes of a container.<br>

**docker ps**: Shows the containers that are runing.<br>

**docker ps -a**: Show the containers that ran recently. Most recent first, also show the stopped containers.<br>

**docker exec -it containerId sh**: _exect_ executes a command in a container that is currently running, the _-it_ is for interactive terminal and _sh_ is for shell, also we can use _bash_ instead of shell.<br>

**docker stop containerId**: Stops the given container but not remove it.<br>

**docker start idContainer**: Start a container in the background (don't show the logs). Start will start any stopped containers (with the data)<br>

**docker run -d --rm -p 8000:80 -v /Users/cristofer/Desktop/docker/nginx:/usr/share/nginx/html --name my-nginx nginx**: Using the volume that we specified. Bind mount.<br>

**docker volume ls**: Shows the volumes that we have.<br>

**docker volume create volumeName**: Creates a new volume with the given name.<br>

**docker run -d --name db --mount src=dbdata,dst=/data/db mongo**: Mounts a volume (dbdata is the name of the volume, /data/db is the path where mongo stores its data).<br>

**docker run -d --rm --mount source=volumeName,target=routeToBeMount imageName**: Mounts a new volume in the container, no all the changes that we make to the target route will be saved in the volume, and not matter if we remove the container, all the data is saved in the volume.<br>

**docker volume rm volumeName**: Removes the given volume.<br>

**docker cp my_route/file.txt container_name:/route_to_copy/new_file_name.txt**: Copy a file into the indicated container.<br>

**docker cp container_name:/route/file_name.txt my_route/new_name_file.txt**: Copy a file from a container to our host machine.<br>

**docker build -t my-own-name:1.0 .**: Build the image with a giving tag.<br>

**docker login**: Connect to Docker Hub.<br>

**docker tag old-name cristofernava/new-name:v2**: Change the old tag (container name) for the new one indicated.<br>

**docker push cristofernava/new-name:v2**: Upload the image to our profile in Docker Hub.<br>

**docker network ls**: Show the networks.<br>

**docker network create my_network_name**: Create a network with the given name.<br>

**docker network create --attachable my_network_name**: Allow others containers to connect to this network.<br>

**docker network connect network_name container_name**: Connects the indicated container to the indicated network.<br>

**docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/test platziapp**<br>

**docker stast**: Useful stats about containers.<br>

<hr>
<br>
<h1>Docker Compose</h1>
Compose is a tool for defining and runnig multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. With this we can describe the architecture of our app.<br>

**vim docker-compose.yaml**: Create a new Docker compose file.<br>

**docker-compose up -d**: _up_ up the services in the the .yaml file. <br>

**docker-compose down**: Stops the current Docker Compose.<br>

<hr>
<br>
<h1>Kubernetes Terminology</h1>

**Kubernetes cluster**: A collections of nodes + a master to manage them.<br>

**Node**: A virtual machine that will run our containers.<br>

**Pod**: More or less a running container. Technically, a pod can run multiple containers (we don't do this). All the containers of the same pod share the same network spacename.<br>

**Deployment**: Monitors a set of pods, make sure they are running and restarts them if they crash.<br>

**Service**: Provides an easy-to-remember URL to access a running container.<br>

<hr>
<br>
<h1>Kubernetes Config Files</h1>

- Tells Kubernetes about the different Deployments, Pods, and Services (referred to as 'Objects') that we want to create.<br>
- Written in YAML syntax.<br>
- Always store files with your projects source code, they are documentation!<br>
- We can craete Objects without config files - **DO NOT DO THIS**. Config files provide a precise definition of what your cluster is running.<br>
- Kubernetes docs will tell you to run direct commands to create objects - only do this for testing purposes.<br>
- Blog posts will tell you to run direct commands to create objects - close the blog post!<br>

<h2>Basic Commands</h2>

**kubectl get pods**: Print out information about all of the running pods.<br>
**kubectl exec -it [pod_name] [cmd]**: Execute the given command in a running pod.<br>
**kubectl logs [pod_name]**: Print out logs from the given pod.<br>
**kubectl delete pod [pod_name]**: Deletes the given pod.<br>
**kubectl apply -f [config file name]**: Tells Kubernetes to process the config.<br>
**kubectl describe pod [pod_name]**: Print out some informatio about the running pod.<br>
**kubectl get deployments**: List all the running deployments.<br>
**kubectl describe deployment [depl name]**: Print out details about a specific deployment.<br>
**kubectl apply -f [config file name]**: Crate a deployment out of a config file.<br>
**kubectl delete deployment [depl_name]**: Delete a deployment.<br>
**kubectl rollout restart deployment [depl_name]**: Update a deploy.<br>

<h3>Services</h3>
Services provide networking between pods.<br>
Types of services:<br>

- **Cluster IP**: Set up an easy-to-remember URL to access a pod. Only exposes pods in the cluster.<br>
- **Node Port**: Makes a pod accessible from outside the cluster. Usually only used for dev purposes.<br>
- **Load Balancer**: Makes a pod accessible from outside the cluster. This is the right way to expose a pod to the outside world.<br>
- **External Name**: Redirects an in-cluster request to a CNAME url... don't worry about this one.<br>

<br>
<h3>Building an alias</h3>

**code ~/.zshrc**: To open the config file.<br>
**source ~/.zshrc**: To restart the terminal.<br>

<h3>Change the /etc/hosts</h3>
For Nginx Ingress we need to set a host, so we have to change the hosts of our computer in order to access to our app and no the given domain in the web.
Just open the file **code /etc/hosts** and add at the end of the file **127.0.0.1 posts.com**

**code ~/.zshrc**: To open the config file.<br>
**source ~/.zshrc**: To restart the terminal.<br>
