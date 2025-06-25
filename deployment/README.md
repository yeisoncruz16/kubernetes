# Deployment Example

This repository contains a Kubernetes deployment configuration for NGINX.

## Files

- `deployment-nginx.yaml`: Kubernetes manifest to deploy an NGINX server.

## What You Have

The `deployment-nginx.yaml` file defines:
- A Deployment resource that manages NGINX pods.
- Configuration for the number of replicas, container image, and ports.

## How to Use

1. **Apply the Deployment:**
    ```sh
    kubectl apply -f deployment-nginx.yaml
    ```

2. **Verify the Deployment:**
    ```sh
    kubectl get deployments
    ```

    ```
    NAME     READY   UP-TO-DATE   AVAILABLE   AGE
    server   1/3     3            1           3s
    ```

    - *READY*: Shows how many pod replicas are currently ready to serve requests. Since no custom readiness probe is defined, a pod is considered ready once its container is running.
    - *UP-TO-DATE*: Indicates the number of pods that have been updated to the latest deployment specification.
    - *AVAILABLE*: Displays the number of pods that are both ready to handle traffic.

    ```
    kubectl get pods
    ```

    *Note*: Pod name is composed using the Deployment name, replicaSet name and rand string: `${deployment-name}-${replica-set-name}-${random-name}`

    ```
    kubectl get rs
    ```

    *Note*: Deployment creates a replicateSet in background, we shouldn't not manage it



## Comparison to ReplicaSet

A **Deployment** offers several advantages over a plain **ReplicaSet**:

- **Rollouts**: Deployments manage rolling updates, allowing you to update the application version with zero downtime by gradually replacing old pods with new ones.
- **Versions**: Deployments keep track of the history of ReplicaSet revisions, making it easy to see which versions have been deployed.
- **Rollbacks**: If a new deployment causes issues, you can quickly revert to a previous stable version using `kubectl rollout undo`.
- **Automatic updates**: Deployments automatically update pods when the deployment specification changes, ensuring the desired state is always maintained.
- **Pause and resume**: You can pause a rollout to apply multiple changes and then resume when ready, providing more control over updates.
- **Status tracking**: Deployments provide detailed status and progress information, making it easier to monitor and troubleshoot updates.

In contrast, a ReplicaSet only ensures a specified number of pod replicas are running, but does not provide versioning, rollouts, or rollback capabilities.

## Cleanup

To remove the deployment:
```sh
kubectl delete -f deployment-nginx.yaml
```
