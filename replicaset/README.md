# ReplicaSet Example

This guide explains how to run the `replicaset.yaml` file to create a ReplicaSet in Kubernetes.

## Steps

1. **Apply the ReplicaSet manifest:**

    ```sh
    kubectl apply -f replicaset.yaml
    ```

2. **Verify the ReplicaSet and Pods:**

    ```sh
    kubectl get rs
    kubectl get rs server # Filter by my replicaSet
    kubectl get pods
    ```

    *Note*: Pod name is composed using the replicaSet name and rand string: `${replica-set-name}-${random-name}`
    ```
    NAME           READY   STATUS    RESTARTS      AGE
    server-dkftt   1/1     Running   0             8m4s
    server-fwgnd   1/1     Running   0             8m4s
    server-lrwfm   1/1     Running   0             8m4s
    server-qwbnk   1/1     Running   0             8m30s
    server-v9bvz   1/1     Running   0             8m4s
    ```

3. Verify nginx is running:
     ```sh
     kubectl exec -it server-dkftt -- bash
     # Then
     curl localhost
     ```

4. **To delete the ReplicaSet:**

    ```sh
    kubectl delete -f replicaset.yaml
    ```

## ReplicaSet limitations

The main limitation of a ReplicaSet is that it does **not** update existing Pods when you modify the Pod template in your manifest file. If you change the container image, environment variables, or other Pod specifications, the ReplicaSet will not automatically replace or update the running Pods. You must manually delete the old Pods to have the ReplicaSet create new ones with the updated configuration.

**Other limitations:**

- **No rolling updates:** ReplicaSet does not support rolling updates or rollbacks natively. For declarative updates and versioned deployments, use a Deployment controller.
- **Limited lifecycle management:** ReplicaSet only ensures the specified number of Pods are running; it does not manage application rollout strategies or history.
- **No direct version tracking:** ReplicaSet does not keep track of previous versions of Pods, making it harder to revert changes.
- **Not intended for direct use:** In most production scenarios, ReplicaSets are managed indirectly by Deployments, which provide more advanced features.

For most use cases, prefer using a Deployment, which manages ReplicaSets and provides advanced update and rollback capabilities.

## Notes

- Make sure `replicaset.yaml` is in your current directory.
- Edit `replicaset.yaml` to customize the ReplicaSet as needed.
