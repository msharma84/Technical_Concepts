# Kubernetes Cheat Sheet

A cheat sheet for Kubernetes commands.

## Cluster Info

- Get clusters
```
kubectl config get-clusters
```

- Get cluster info.
```
kubectl cluster-info
  Kubernetes master is running at https://172.17.0.58:8443
```

- Check information of current cluster
```
kubectl config view --minify
```

## Contexts

A context is a cluster, namespace and user.

- Get all context :
```
kubectl config get-contexts
```

- Get the current context.
```
kubectl config current-context
```

- Switch current context.
```
kubectl config use-context <context-name> or <arn>
```

- Check information of all config
```
kubectl config view
```

- Set default namesapce
```
kubectl config set-context $(kubectl config current-context) --namespace=<namespace>
```

## Get Commands

```
kubectl get all
kubectl get namespaces
kubectl get configmaps
kubectl get nodes
kubectl get pods
kubectl get rs
kubectl get svc kuard
kubectl get endpoints kuard
```

Additional switches that can be added to the above commands:

- `-o wide` - Show more information.
- `--watch` or `-w` - watch for changes.

## Namespaces

- `--namespace` - Get a resource for a specific namespace.

You can set the default namespace for the current context like so:

```
kubectl config set-context $(kubectl config current-context) --namespace=my-namespace
```

- Get namespace
```
kubectl get namespace
```

Get all namespace
```
kubectl get all -n <namespace>
```

## Pod

- Get a particular pod of a particular namespace
```
kubectl get pods -n <namespace>
kubectl get pods -o wide -n <namespace>
kubectl describe pods <pod-name> -n <namespace>
```

- Get all pod inside a cluster
```
kubeclt get pods -A
```

