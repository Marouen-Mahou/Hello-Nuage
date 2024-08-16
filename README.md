# Introduction
This project involves a Kubernetes technical test where we applied our expertise in containerization and Kubernetes to deploy and manage a Vue.js web application. Through this project, we demonstrated our ability to integrate and orchestrate a modern web framework within a Kubernetes environment, showcasing both our technical proficiency and practical understanding of cloud-native technologies.

# Prerequisites
To be able to test the application and the deployment properly you need a set of tools to be installed:

- [docker](https://www.docker.com/)
- [kubernetes](https://kubernetes.io/)
- [helm](https://helm.sh/)
- [node.js](https://nodejs.org/)
- [vue.js](https://vuejs.org/)

# Run the web application in local
1- Run this command to install all the needed packages for the application
```
npm install
```

2- Run this command to serve the application on http://localhost:8080/
```
npm run serve
```
![image](https://github.com/user-attachments/assets/40a97aa6-32b5-4200-b06e-231dad2aef36)

3- Run this command to build the production environement into /dist directory
```
npm run build
```

# Build the docker image

1- Run this command to build the docker image
```
docker build . -t marouenmahou/hello-nuage
```

![image](https://github.com/user-attachments/assets/c77e5416-0fd2-41e2-a1e8-ff824a64c527)


2- Run this command to run the container of the built image
```
docker run -p 8080:80 marouenmahou/hello-nuage
```

3- Run this command to check if the container is running
```
docker ps
```
![image](https://github.com/user-attachments/assets/8a6e7fb9-0fb2-4d40-af7c-6a37922b1525)


4- If you want to push the image to dockerhub registry run these two commands
```
docker login
docker push marouenmahou/hello-nuage
```
 ***Note:*** you need to change **marouenmahou** by your dockerhub repository name

 ![image](https://github.com/user-attachments/assets/e068f6d3-e034-448c-a176-ca7dbd2ff4ab)


# Deployment
We will use a Helm chart to deploy a Kubernetes cluster that will host our web application. This approach enables streamlined management and configuration of the deployment, ensuring a robust and scalable environment for our application.

## Kubernetes Objects
- Deployment
- Service
- Ingress
- NameSpace
- NetworkPolicy
- Horizontal Pod Autoscaling (HPA)

## Helm Chart Deployment

After editing the values of the chart you run this command to install the chart with all the kubernetes objects
```
helm install hellonuage . -f values.yaml
```
![image](https://github.com/user-attachments/assets/243d3a35-489d-4b23-b2c7-c43272b4dd59)

To verify the chart installation run this command
```
helm list
```
![image](https://github.com/user-attachments/assets/1159e8d9-3ed6-4e71-a602-c9216f3f2278)

To check running pods run this command
```
kubectl get pods -n hello-nuage
```
![image](https://github.com/user-attachments/assets/a7330b3e-9a45-4f6e-8d67-aee5a34a3ffe)

To uninstall the chart simply run this command
```
helm uninstall hellonuage
```

## Self-healing demonstration

To verify the self-healing capabilities of our deployment, we will first ensure that the deployment reaches the desired number of replicas. Once stabilized, we'll deliberately delete one of the pods and observe whether the deployment automatically creates a new pod to maintain the specified replica count, thereby demonstrating its resilience and ability to self-recover.

![Self Healing Kubernetes](https://github.com/user-attachments/assets/58053afb-2a31-4d1b-a222-d0513d79ae61)




