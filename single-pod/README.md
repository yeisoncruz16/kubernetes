# NGINX Pod Example

This repository contains a Kubernetes manifest file, `pod-nginx.yaml`, which defines a simple Pod running the NGINX web server.

## File Overview

- **pod-nginx.yaml**:
    Describes a single Pod with one container running the official NGINX image.

## Usage

1. Apply the manifest to your Kubernetes cluster:
     ```sh
     kubectl apply -f pod-nginx.yaml
     ```

2. Verify the Pod is running:
     ```sh
     kubectl get pods
     ```

2. Verify nginx is running:
     ```sh
     kubectl exec -it nginx-pod -- bash
     # Then
     curl localhost
     ```

## Details

- **Image**: Uses the latest official NGINX image from Docker Hub.
- **Ports**: Exposes port 80 inside the container for HTTP traffic.

## Purpose

This example demonstrates how to deploy a basic NGINX server as a standalone Pod in Kubernetes. It is useful for learning and testing purposes.
