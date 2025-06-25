# Service Example

This file defines a Kubernetes Service for exposing an NGINX deployment.

## Overview

- **Type:** Service
- **Purpose:** Exposes NGINX pods to internal/external traffic
- **Typical Use:** Load balancing and stable networking for NGINX

## Example Usage

Apply the service:

```sh
kubectl apply -f service-nginx.yaml
```

## Related Files

- `deployment-nginx.yaml`: NGINX Deployment definition

## Notes

- The request will be distributed using Round-robin

## Troubleshooting

- In case you see the error "Exiting due to SVC_UNREACHABLE: service not available: no running pod for service nginx-service found", make sure you are using the correct label selection for pod+deployment+service
    - `kds nginx-service`
    - `Endpoints` should look like `Endpoints: 10.244.205.201:80,10.244.120.71:80,10.244.205.202:80` which means the list of the pods that are going to receive the traffic

## Limitations

When using minikube locally you will need to use the service command `minikube service nginx-service`

## Cleanup

To remove the service:
```sh
kubectl delete -f service-nginx.yaml
```
