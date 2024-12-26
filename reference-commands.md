# Kubernetes Namespace Management Command Reference Guide

### Project Content Table
- [Core Namespace Operations](#core-namespace-operations)
- [Resource Management](#resource-management)
- [Advanced Operations](#advanced-operations)
- [Monitoring and Troubleshooting](#monitoring-and-troubleshooting)

> **Author**: [Md Toriqul Islam](https://linkedin.com/in/thetoriqul)  
> **Description**: Comprehensive command reference for Kubernetes namespace management  
> **Note**: Verify your cluster context before executing commands

## Core Namespace Operations

### Creating Namespaces

```bash
# Create namespace using kubectl
kubectl create namespace my-namespace

# Create namespace from YAML file
kubectl apply -f example-namespace.yaml

# Verify namespace creation
kubectl get namespace my-namespace
```

### Viewing Namespaces

```bash
# List all namespaces
kubectl get namespaces

# Get detailed namespace information
kubectl describe namespace my-namespace

# View namespace in YAML format
kubectl get namespace my-namespace -o yaml
```

## Resource Management

### Pod Operations in Namespaces

```bash
# Create pod in specific namespace
kubectl apply -f mypod.yaml --namespace=my-namespace

# List pods in namespace
kubectl get pods --namespace=my-namespace

# Get pod details
kubectl describe pod mypod --namespace=my-namespace

# Verify pod status
kubectl get pod mypod -n my-namespace -o wide
```

### Resource Viewing

```bash
# View all resources in namespace
kubectl get all --namespace=my-namespace

# View specific resource types
kubectl get pods,services,deployments --namespace=my-namespace

# Watch resource changes
kubectl get pods -n my-namespace --watch
```

## Advanced Operations

### Namespace Management

```bash
# Set default namespace for context
kubectl config set-context --current --namespace=my-namespace

# View current namespace context
kubectl config view --minify | grep namespace:

# Create namespace with resource quota
kubectl create namespace my-namespace
kubectl apply -f quota.yaml -n my-namespace
```

### Resource Quota Management

```bash
# Apply resource quota to namespace
kubectl apply -f - <<EOF
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: my-namespace
spec:
  hard:
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
EOF

# View resource quotas
kubectl get resourcequota -n my-namespace
```

## Monitoring and Troubleshooting

### Namespace Health Checks

```bash
# Check namespace status
kubectl get events --namespace=my-namespace

# View namespace resource usage
kubectl top pod --namespace=my-namespace

# Check pod logs in namespace
kubectl logs -f pod-name --namespace=my-namespace
```

### Cleanup Operations

```bash
# Delete specific resources
kubectl delete pod mypod --namespace=my-namespace

# Delete all resources in namespace
kubectl delete all --all --namespace=my-namespace

# Delete namespace and all resources
kubectl delete namespace my-namespace

# Verify namespace deletion
kubectl get namespace | grep my-namespace
```

## Learning Notes

1. Always verify the target namespace before executing commands
2. Use resource quotas to prevent resource exhaustion
3. Implement proper naming conventions for namespaces
4. Regular cleanup of unused namespaces is essential
5. Monitor namespace resource utilization

---

> 💡 **Best Practice**: Use declarative YAML files for namespace and resource creation to maintain version control

> ⚠️ **Warning**: Deleting a namespace will delete ALL resources within it

> 📝 **Note**: Keep namespace names clear and meaningful for better organization