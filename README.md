# python-docker-eks
This project will deplopy Python code from Local Machine to Kubernetes in Cloud.

### Container Lifecycle:

* Running container in local machine.
* Containerizing the program.
* Run the container locally.
* Deploy the container to AWS.
* Expose the container.
* Scale the container. 

### Requirements:

* Homebrew `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
* Python (latest v3.9, pip, and setup tools) `brew install python`
* Docker `brew install docker`
* Eksctl `brew install eksctl`
* clone repository `git@github.com:jcquiles/python-docker-eks.git`

#### Step 1: 
* install flask `pip install flask` or `python3 -m pip install Flask==1.1.2`
* write and run python flask app from server.py `server.py`
---------------------------------------------------------------------------
* **Flask is a web framework, it's a Python module that lets you develop web applications easily. It's has a small and easy-to-extend core.**
---------------------------------------------------------------------------
* check localhost:500 to check if flask program is returning "hello world".

### Step 2: 
* containerize code by running `Dockerfile`
----------------------------------------------------------------------------
* **Dockerfile is a text document that contains all the commands to create an image and package a container.**
-----------------------------------------------------------------------------

### Step 3:
* build image `docker build -t flaskapp`
* verify image is created `docker images`
* run the container `docker run -d -p 5000:5000`
* `-d` to keep the container running in the background.
* `p` to publish the port 5000 to the localhost 5000.
------------------------------------------------------------------------------
* **The first 5000 is the container port.**
* **The second 5000 is the host port.**
-------------------------------------------------------------------------------
* verify the container is created `docker ps`
* check to see if the container is running `docker ps -a`
* **if not running check logs of the container id with `docker logs <CONTAINER-ID>`**

### Step 4:
* create public repository in your Docker Hub.
* login to Docker `docker login` then `docker images`
* tag Docker image `docker tag <image-ID> <docker-account-name/dockerhub-repo-name>`
---------------------------------------------------------------------------------
* **if you dont specify a tag it will pick up the latest tag**
---------------------------------------------------------------------------------
* push image `docker push <docker-username/dockerhub-repo-name>`

### Step 5:
* create eks cluster `eksctl create cluster`
---------------------------------------------------------------------------------
* **this may take several minutes to create**
---------------------------------------------------------------------------------
* deploy deployment manifest for cluster `kubectl apply -f flaskdeploy.yaml`
* deploy service mainfest for cluster `kubectl apply -f flasksvc.yaml`
* verify service is working by testing the load balancer service.