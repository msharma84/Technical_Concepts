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
