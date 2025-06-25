# Kubernetes with Minikube

This project uses **Kubernetes** for container orchestration, running locally with **Minikube**.

## Setup

- **Minikube** is used to create a local Kubernetes cluster.
- The cluster is configured with two worker nodes.
- The **Calico** CNI (Container Network Interface) is used for networking and necessary for the second node.

## Steps

1. Start Minikube with Calico as the CNI:
    ```sh
    minikube start --cni=calico
    minikube node add # This line is adding the second node
    ```
2. Verify the nodes:
    ```sh
    kubectl get nodes
    ```

## Recommendations

- Enable kubectl plugin for zsh.
    - `vim ~/.zshrc`
    - add kubectl in the plugins section `plugins=(git kubectl)`
- Enable kubectx for context and namespace management
    - `brew install kubectx`
    - `kubectx minikube`
    - `kubens ${your-namespace}`


## Notes

- Calico provides advanced networking and network policy support.
- This setup is ideal for local development and testing Kubernetes workloads.
