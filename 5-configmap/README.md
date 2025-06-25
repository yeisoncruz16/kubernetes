# ConfigMap Example

This file demonstrates how to use a Kubernetes ConfigMap with an Nginx deployment.

## What it does

- **Creates a ConfigMap**: Stores custom Nginx configuration data.
- **Deploys Nginx**: Launches an Nginx Deployment using the official image.

## Why use a ConfigMap?

ConfigMaps allow you to decouple configuration artifacts from image content, making your deployments more flexible and manageable.

## How to use

1. Apply the ConfigMap:
    ```sh
    kubectl apply -f cm-deployment-nginx.yaml
    ```

2. The deployment will use the configuration from the ConfigMap automatically.

3. List the current Pods
    ```sh
    kubectl get pod | grep server-cm
    ```

4. Verify the env variable
    ```sh
    kubectl exec -it server-cm-754b4dbd8d-knc9c -- bash
    # Then
    env | grep WELCOME_MESSAGE
    # Or
    echo $WELCOME_MESSAGE
    ```

## Limitations without volume
- When the ConfigMap is updated, environment variables injected into Pods are **not** updated automatically. You must restart the Pods to pick up changes.
- Environment variables from ConfigMaps are only set at Pod startup; dynamic updates are not supported.
- ConfigMap changes do **not** propagate to running containers when used as environment variables.
- Sensitive data should not be stored in ConfigMaps; use Secrets for confidential information.
- Large configuration files or binary data are not suitable for ConfigMaps.
- If the ConfigMap is deleted, Pods depending on it may fail to start or restart.

## Customization

Edit the ConfigMap section to change Nginx settings without rebuilding the Docker image.

## Cleanup

To remove the service:
```sh
kubectl delete -f cm-deployment-nginx.yaml
```
