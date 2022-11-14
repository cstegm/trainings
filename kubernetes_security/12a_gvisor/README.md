# gVisor

## Create Runtime Class
Create a different runtime handler, called runsc (gvisor).

```bash
cd ./12a_gvisor

kubectl get runtimeclass ## No resources found

kubectl apply -f runtime_class.yaml

kubectl get runtimeclass
```

Create the pods with `gvisor` runtime class and default `runc` class:

```bash
kubectl create -f pod_runsc.yaml
kubectl create -f pod_runc.yaml
```

## Check if gVisor is working

Check the pod's kernel version with gvisor

```bash
kubectl exec -it nginx-gvisor -- /bin/bash

uname -r   # shows kernel release

exit
```

Check the pod's kernel version without gvisor

```bash
kubectl exec -it nginx -- /bin/bash

uname -r   # shows kernel release

exit
```

Check node's kernel version

```bash
uname -r
```

Note that gVisor has a different kernel version that the node and the other pod.

## Cleanup

```bash
kubectl delete pod nginx
kubectl delete pod nginx-gvisor
```
