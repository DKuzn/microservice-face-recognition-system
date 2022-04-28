# Microservice face recognition system

## How to build containers in local registry?

```bash
docker-compose build
```

## How to run microservices in local kubernetes cluster?

Install minikube and run in terminal:

```bash
minikube start
```

Add ingress addon:

```bash
minikube addons enable ingress
```

Run command below and follow instructions:

```bash
minikube docker-env
```

Now you can build containers in minikube registry:

```bash
docker-compose build
```

Next you need to apply kubernetes resoures:

```bash
cd kubernetes
kubectl apply -f ./secrets.yaml
kubectl apply -f ./deployments
kubectl apply -f ./services
kubectl apply -f ./ingress.yaml
```

Now you can access to database server to fill it, just forward a port:

```bash
kubectl port-forward --address 0.0.0.0 service/database 3306:3306
```

To use web app, again forward the port to local network:
```bash
kubectl port-forward --address 0.0.0.0 service/face-recognition-app 80:80
```
