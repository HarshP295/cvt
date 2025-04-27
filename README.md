# cvt

Experiment No. 2


AIM:Run and execute any 6 docker commands and comment on it.


Theory:

Procedure:
Step1: do exp 3 
Step 2: 
Build an image from Dockerfile
docker build -t image_name path_to_docker_file
eg.docker build -t my_app .

List all local images
docker images
eg. docker images ls

Pull an image
docker pull image_name:tag
eg:docker pull nginx:latest

Run a container
docker run container_name
eg.docker run my_app

List all Running container
docker ps
docker ps -a (for running and stopped containers)

Stop a container
docker stop container_name or id
docker start container_name or id

Remove a container
docker rm container_name or id

Inspect a container
docker inspect my_container



Experiment No. 3

AIM:Create a docker file , docker image and run the container from the image file.

Procedure:
Step1:Clone experiment 2
Step2:Create a Dockerfile into the project structure without any extensions.
Step3:Include the following code into the Dockerfile:
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY index.html style.css script.js /usr/share/nginx/html/
EXPOSE 80
Step4:Run the following command in the terminal
docker build -t (name of project) .
Step5:Run the container
docker run -d -p 3000:80 (name of project)
Step6:You can go to docker desktop and can see your image running.Also to the port where your image is running.


Experiment No. 4
AIM:Pull an image from a docker hub and perform the following tasks : 
	a) create a container, b) run the container, 3) stop the container

Procedure:
🔹 1. Pull the image from Docker Hub
docker pull nginx
✔ This command fetches the nginx image from Docker Hub and stores it locally.
🔹 2. Check if the image is pulled
docker images

🔹 3. Create and run a container from the image
docker run -d --name my-nginx -p 8080:80 nginx
-d runs the container in detached mode (in the background)


--name my-nginx gives the container a name


-p 8080:80 maps host port 8080 to container port 80
✔ Now visit http://localhost:8080 in your browser. You’ll see the Nginx welcome page served from inside the Docker container.
🔹 4. Check running containers
docker ps
✔ This will show your running container like:
CONTAINER ID   IMAGE   COMMAND   STATUS   PORTS
<id>           nginx   ...       Up       0.0.0.0:8080->80/tcp
🔹 5. Stop the container
docker stop my-nginx
✔ This will stop the running container named my-nginx.
🔹 6. (Optional) Restart or Remove the container
Restart: docker start my-nginx
Remove container:  docker rm my-nginx

Experiment No. 5
Aim:Create a master node and worker node in kubernetes. Run any 6 commands of kubernetes.


Theory:
Procedure:
Master node and Worker node are already created in KillerCoda.
# 1. Check Nodes
kubectl get nodes
# 2. Create a Pod
kubectl run nginx-pod --image=nginx
# 3. Get Pod Details
kubectl get pods
kubectl describe pod nginx-pod
# 4. Expose Pod as Service
kubectl expose pod nginx-pod --port=80 --type=NodePort
# 5. Get Services
kubectl get svc
# 6. Delete Pod
kubectl delete pod nginx-pod

Experiment No.6
Aim:Create a pod in kubernetes , find the ip address and do the troubleshooting via log.
Step 2: Create a Pod YAML File
Use nano or vim to create a pod config:
nano mypod.yaml
Paste this content:{
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: nginx
    ports:
    - containerPort: 80
}
Save and exit (Ctrl + O, Enter, Ctrl + X).
Step 3: Create the Pod
kubectl apply -f mypod.yaml

Check pod status:
kubectl get pods

Step 4: Get Pod IP Address
kubectl get pod myapp-pod -o wide

This shows the Pod IP under the IP column.
Step 5: Troubleshoot Using Logs
If the pod is running:
kubectl logs myapp-pod

If the pod crashes, you can check logs of the previous container:
kubectl logs myapp-pod --previous

If the pod isn't starting, describe it:
kubectl describe pod myapp-pod
