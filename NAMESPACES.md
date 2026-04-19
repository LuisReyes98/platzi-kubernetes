# Creating a Pod in a Specific Namespace

There are several ways to create a pod in a specific namespace in Kubernetes.

## Option 1: Using `--namespace` flag (imperative)

```bash
# Create a pod directly with kubectl run
kubectl run my-pod --image=nginx --namespace=my-namespace

# Short form
kubectl run my-pod --image=nginx -n my-namespace
```

## Option 2: Specifying namespace in the YAML manifest (declarative)

Add the `namespace` field under `metadata`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: my-namespace    # 👈 specify here
  labels:
    app: my-app
spec:
  containers:
  - name: my-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

Then apply it:

```bash
kubectl apply -f pod.yaml
```

## Option 3: Using `-n` with `kubectl apply` (overrides YAML)

If your YAML doesn't specify a namespace, you can pass it at apply time:

```bash
kubectl apply -f pod.yaml -n my-namespace
```

> ⚠️ **Note:** If the YAML already has a `namespace` field, the one in the YAML wins over the `-n` flag in some scenarios. Be explicit to avoid confusion.

## Before creating: make sure the namespace exists

The namespace must exist before creating the pod, otherwise you'll get an error.

```bash
# Check if the namespace exists
kubectl get namespaces

# Create it if it doesn't
kubectl create namespace my-namespace

# Or declaratively
kubectl apply -f - <<EOF
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
EOF
```

## Verifying the pod was created in the correct namespace

```bash
# List pods in the specific namespace
kubectl get pods -n my-namespace

# Describe the pod to confirm
kubectl describe pod my-pod -n my-namespace

# See pods across ALL namespaces
kubectl get pods --all-namespaces
# or shorter:
kubectl get pods -A
```

## Bonus: Set a default namespace for your context

If you're working in a specific namespace a lot, avoid typing `-n my-namespace` every time by setting it as default:

```bash
# Set the default namespace for the current context
kubectl config set-context --current --namespace=my-namespace

# Verify
kubectl config view --minify | grep namespace
```

After this, commands like `kubectl get pods` will automatically use `my-namespace`.

## Complete example

```bash
# 1. Create the namespace
kubectl create namespace dev

# 2. Create a pod in it (imperative)
kubectl run nginx-pod --image=nginx -n dev

# 3. Verify
kubectl get pods -n dev
```

Or declaratively with a manifest:

```yaml
# nginx-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  namespace: dev
spec:
  containers:
  - name: nginx
    image: nginx:latest
```

```bash
kubectl apply -f nginx-pod.yaml
kubectl get pods -n dev
```

## Quick tip

Pods are rarely created directly in production. Usually you'd create a **Deployment**, which manages pods for you. The namespace rules are the same — just specify `namespace` in the metadata or use `-n` at apply time.