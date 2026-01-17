In **Kubernetes (k8s)**, a **Namespace** is a **logical partition** used to **organize, isolate, and manage resources** within a cluster.

### In simple words:

A **Namespace** is like a **folder** inside a Kubernetes cluster that separates resources.

### Why Namespaces are used:

* Organize resources (dev, test, prod)
* Avoid **name conflicts** (same resource names can exist in different namespaces)
* Apply **resource limits** (CPU, memory)
* Apply **RBAC access control**
* Better cluster management for large environments

### Key points:

* Every Kubernetes resource belongs to **one namespace** (except cluster-wide resources)
* Default namespaces exist by default
* Same resource name can be reused in different namespaces

### Default Kubernetes namespaces:

* **default** – resources created without specifying a namespace
* **kube-system** – Kubernetes system components
* **kube-public** – public data (mostly read-only)
* **kube-node-lease** – node heartbeat information

### Example:

You can have:

* `dev` namespace → development apps
* `test` namespace → testing apps
* `prod` namespace → production apps

### Simple analogy:

* Kubernetes Cluster = Building
* Namespace = Floor
* Pods/Services = Rooms on that floor

### Example command:

```bash
kubectl get namespaces
```

Create a namespace:

```bash
kubectl create namespace dev
```

Use a namespace:

```bash
kubectl get pods -n dev
```

**Important:**
Namespaces do **not** provide strong security isolation like VMs; they are mainly for **logical separation and management**.
