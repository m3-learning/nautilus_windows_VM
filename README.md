# nautilus_windows_VM

# 0. set namespace

```bash
kubectl config set-context --current --namespace=m3learning
```

# 1. Adding the PV

```bash
kubectl apply -f pv.yaml
```

# 2. Creating the Drive

```bash
kubectl apply -f drive.yaml
```