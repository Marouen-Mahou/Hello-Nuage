# Introduction
This project is about a kubernetes technical test where we have implemented our contenairzation and kubernetes knowledge in a Vue.js web application. 

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

3- Run this command to build the production environement into /dist directory
```
npm run build
```

# Build the docker image

1- Run this command to build the docker image
```
docker build . -t marouenmahou/hello-nuage
```

2- Run this command to run the container of the built image
```
docker run -p 8080:80 marouenmahou/hello-nuage
```

3- Run this command to check if the container is running
```
docker ps
```

4- If you want to push the image to dockerhub registry run these two commands
```
docker login
docker push marouenmahou/hello-nuage
```
 ***Note:*** you need to change **marouenmahou** by your dockerhub repository name

# Deployment
We are going to use a helm chart to deploy a kubernetes cluster where our web application will live.

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
helm install hellonuage . -f values.yaml -n hello-nuage
```

To verify the chart installation run this command
```
helm list
```

To check running pods run this command
```
kubectl get pods -n hello-nuage
```

To check running HPA run this command
```
kubectl get hpa -n hello-nuage
```

To uninstall the chart simply run this command
```
helm uninstall hellonuage
```

## Self-healing demonstration

To test the self-healing of our deployment and after the deployment reachs the desired number of replicas, we will delete one pod and we check if the deployment creates a new pod to match the number of replicas.

![Self Healing Kubernetes](https://github.com/user-attachments/assets/58053afb-2a31-4d1b-a222-d0513d79ae61)




