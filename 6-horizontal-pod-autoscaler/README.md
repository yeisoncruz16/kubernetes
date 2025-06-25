# Horizontal Pod Autoscaler (HPA)

This folder contains a Kubernetes manifest file: `hpa-deployment-nginx.yaml`. This file demonstrates how to deploy an NGINX server with Horizontal Pod Autoscaler (HPA) enabled.

## What `hpa-deployment-nginx.yaml` Does

- **Deployment:** Creates a Deployment running the NGINX web server.
- **Resource Requests/Limits:** Sets CPU requests/limits for the pods.
- **HPA:** Configures an HPA to automatically scale the number of NGINX pods based on CPU utilization.

## How to Run

1. **Apply the Manifest:**
    ```sh
    kubectl apply -f hpa-deployment-nginx.yaml
    ```

2. **Verify the Deployment:**
    ```sh
    kubectl get deployments
    kubectl get pods
    ```

3. **Monitor Scaling:**
    ```sh
    kubectl get hpa
    ```

## Considerations

If you are using Minikube you can enable metrics using
```sh
minikube addons enable metrics-server
```

## Cleanup

To remove the service:
```sh
kubectl delete -f hpa-deployment-nginx.yaml
```
