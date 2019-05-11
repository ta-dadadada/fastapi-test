# fastapi-test

Test FastAPI (the awesome web framework of Python), and deploy kubernetes.

## Architecture

* The k8s pods consist of Python application (written by FastAPI, running by uvicorn) and Envoy as sidecar
* Envoy loads its config from mounted volume by k8s ConfigMap
  * The config is written in `configmap.yaml` directly
* The k8s service expose **nodePort**

## Deploy

```sh
kubectl apply -f configmap.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

## Examine

You can test easily if minikunbe.

```sh
$ curl $(minikube service api-service --url)/health
```