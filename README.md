# Nautilus Windows VM

## Requirements

- [Krew](https://krew.sigs.k8s.io/docs/user-guide/setup/install/)
## 1. Install Krew

```bash
(
  set -x; cd "$(mktemp -d)" &&
  OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
  KREW="krew-${OS}_${ARCH}" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
  tar zxvf "${KREW}.tar.gz" &&
  ./"${KREW}" install krew
)
```

### 2. Restart your shell

### 3. Add Krew to your PATH

```bash
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```

### 4. Check if Krew is installed

```bash
kubectl krew version
```

- [vritclt](https://kubevirt.io/user-guide/user_workloads/virtctl_client_tool/)

### 1. Install virtctl

```bash
kubectl krew install virt
```

or 

```bash
# Download the virtctl binary
curl -LO https://github.com/kubevirt/kubevirt/releases/download/v0.41.0/virtctl-v0.41.0-darwin-amd64

# Make the binary executable
chmod +x virtctl-v0.41.0-darwin-amd64

# Move the binary to a directory in your PATH
sudo mv virtctl-v0.41.0-darwin-amd64 /usr/local/bin/virtctl
```



## 0. set namespace

```bash
kubectl config set-context --current --namespace=m3learning
```

## 1. Adding the PV

**NOTE:** This can be somewhat slow.

```bash
kubectl apply -f PV.yaml
```

## 2. Creating the Drive

```bash
kubectl apply -f drive.yaml
```

## 3. Creating the VM

```bash
kubectl apply -f vm.yaml
```

## 4. Starting the VM

```bash
virtctl start winvm
```

## 5. Accessing the VM

```bash
kubectl apply -f virtvnc.yaml
```

## 6. Service accounts and roles

```bash
kubectl apply -f serviceaccounts.yaml 
```

## 7. Ingress

**NOTE:** If necessary you can change the ingress to use a different domain.

```bash
kubectl apply -f ingress.yaml
```

## 8. Secret to hold the password for your virtvnc:

kubectl create secret generic virtvnc-login  --from-literal=auth=jca92::password