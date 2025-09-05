## **Day 1: Why Docker Alone Struggles at Enterprise Scale**

Docker is great for:

- Packaging applications in containers.
    
- Running them consistently anywhere.
    
- Easy developer adoption.
    

But **Docker alone** (without orchestration) lacks several key enterprise capabilities:

---

### **1. Auto-healing**

**Problem:**  
If your container crashes, Docker will stop it.  
You can configure `--restart=always` to restart, but that’s:

- Per-container, manual setup.
    
- Not aware of _application health_ — it doesn’t know if your app is “unhealthy” but still running.
    
- No health probe checks like Kubernetes’ **liveness**/**readiness** probes.
    

**Enterprise Impact:**  
In production, we need automated detection and recovery from:

- App crashes.
    
- Node failures.
    
- Network partitioning.
    

**How Kubernetes solves this:**  
Kubernetes automatically monitors pod health and restarts/replaces failing pods — even moving them to other nodes if needed.

---

### **2. Auto-scaling**

**Problem:**  
Docker alone can’t:

- Increase container count when traffic spikes.
    
- Reduce container count when traffic is low to save cost.
    

**Enterprise Impact:**  
Without auto-scaling:

- You either overprovision (waste money) or underprovision (cause downtime).
    
- Manual scaling = slow response to traffic bursts.
    

**How Kubernetes solves this:**  
Kubernetes **Horizontal Pod Autoscaler (HPA)** scales pods based on CPU, memory, or custom metrics automatically.

---

### **3. Clustering**

**Problem:**  
Docker on its own:

- Runs on a single host.
    
- Has no built-in way to spread workloads across multiple machines.
    
- No central scheduler to distribute workloads.
    

**Enterprise Impact:**  
If the server goes down, _all_ your containers go down with it.  
No high availability, no redundancy.

**How Kubernetes solves this:**  
Kubernetes clusters multiple nodes and schedules pods across them for HA, load distribution, and failover.

---

### **4. Networking & Service Discovery**

(Didn’t list in your points, but worth mentioning.)  
Docker has basic bridge networking, but:

- No built-in service discovery across hosts.
    
- Manual IP management is required when scaling containers.
    

**How Kubernetes solves this:**  
Kubernetes provides:

- Cluster DNS for automatic service discovery.
    
- Load balancing between pods.
    
- Ingress Controllers for HTTP routing.


|Feature|Plain Docker|Kubernetes|
|---|---|---|
|Auto-healing|Only via restart policy (limited)|Full pod health checks + rescheduling|
|Auto-scaling|Manual|HPA/VPA/Cluster autoscaler|
|Clustering|None|Multi-node scheduling & HA|
|Service discovery|Limited (same host only)|Cluster-wide DNS + load balancing|
|Rolling updates|Manual container replace|Automated rolling & rollback|
|Traffic routing|Manual ports|Ingress, Services, LB integration|


## **Classic Problems Solved by Kubernetes (Not Solvable by Plain Docker)**

### **1. High Availability & Auto-healing**

- **Problem with Docker:** If a container crashes, Docker can restart it only if configured (`--restart` flag) — no health probes, no node failure recovery.
    
- **Kubernetes Solution:** Health checks (liveness/readiness probes), automatic pod restarts, and rescheduling to other nodes when a host fails.
    

---

### **2. Automatic Scaling**

- **Problem with Docker:** No way to automatically add/remove containers based on CPU, memory, or traffic.
    
- **Kubernetes Solution:** **Horizontal Pod Autoscaler (HPA)** and **Vertical Pod Autoscaler (VPA)** adjust workloads in real-time.
    

---

### **3. Multi-node Clustering**

- **Problem with Docker:** Runs only on a single node unless you manually set up networking and scheduling (error-prone, not scalable).
    
- **Kubernetes Solution:** Orchestrates workloads across multiple nodes, balancing load and providing redundancy.
    

---

### **4. Service Discovery & Internal Load Balancing**

- **Problem with Docker:** Containers on different hosts can’t discover each other without manual IP/port management.
    
- **Kubernetes Solution:** Built-in **DNS service** so apps can find each other by name, plus built-in load balancing for distributing requests between pods.
    

---

### **5. Rolling Updates & Rollbacks**

- **Problem with Docker:** Updating an app means manually stopping and starting containers, risking downtime.
    
- **Kubernetes Solution:** **Rolling updates** replace containers gradually with zero downtime, and can **rollback** if something fails.
    

---

### **6. Declarative Configuration & Desired State**

- **Problem with Docker:** Mostly imperative — you run containers with commands and scripts, but there’s no “desired state” management.
    
- **Kubernetes Solution:** Declarative YAML manifests tell Kubernetes the desired state; Kubernetes continuously works to match it.
    

---

### **7. Self-healing Network Routing**

- **Problem with Docker:** Networking is limited to a host or requires complex manual overlay networking for multi-host setups.
    
- **Kubernetes Solution:** Automatic **pod IP management**, cross-node networking, and routing via **Services** and **Ingress**.
    

---

### **8. Persistent Storage Management**

- **Problem with Docker:** Containers lose data when they restart unless you manually mount volumes.
    
- **Kubernetes Solution:** **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)** for portable, cluster-managed storage across nodes.
    

---

### **9. Workload Scheduling**

- **Problem with Docker:** No smart scheduler — you decide manually where containers run.
    
- **Kubernetes Solution:** **Scheduler** automatically places pods based on resources, affinity rules, and workloads.
    

---

### **10. Security & Isolation at Scale**

- **Problem with Docker:** Security policies and isolation are manual per-container.
    
- **Kubernetes Solution:** **RBAC**, namespaces, network policies, and secrets management to enforce enterprise-grade security.


### **1. Clustering**

**Problem:**  
Docker on its own:

- Runs on a single host.
    
- Has no built-in way to spread workloads across multiple machines.
    
- No central scheduler to distribute workloads.
    

**Enterprise Impact:**

- If the server goes down, all your containers go down with it.
    
- No high availability, no redundancy.
    

---

### **2. Auto-healing**

**Problem:**  
Docker on its own:

- Only restarts crashed containers if configured with `--restart=always`.
    
- Doesn’t detect if the application is “unhealthy” but still running.
    
- No health probe checks to restart unhealthy services.
    

**Enterprise Impact:**

- Stuck or frozen applications stay broken until manual intervention.
    
- Service downtime increases.
    

---

### **3. Auto-scaling**

**Problem:**  
Docker on its own:

- No built-in way to automatically scale containers up/down based on load.
    
- Scaling must be done manually.
    

**Enterprise Impact:**

- Can’t handle sudden traffic spikes without manual action.
    
- Overprovisioning wastes resources and money.
    

---

### **4. Service Discovery & Networking**

**Problem:**  
Docker on its own:

- Only provides basic networking on the same host.
    
- No cluster-wide DNS naming for services.
    
- Requires manual IP management across hosts.
    

**Enterprise Impact:**

- Difficult to connect microservices running across multiple machines.
    
- Hard to replace/scale services without breaking connections.
    

---

### **5. Rolling Updates & Rollbacks**

**Problem:**  
Docker on its own:

- Updating a container means manually stopping the old one and starting a new one.
    
- No built-in rollback if the new version fails.
    

**Enterprise Impact:**

- Risk of downtime during deployments.
    
- Harder to revert quickly in case of deployment failures.
    

---

### **6. Load Balancing**

**Problem:**  
Docker on its own:

- No built-in HTTP load balancing across multiple containers.
    
- Requires external tools or manual configuration.
    

**Enterprise Impact:**

- Uneven traffic distribution.
    
- Extra complexity in maintaining external load balancers.
    

---

### **7. Storage & State Management**

**Problem:**  
Docker on its own:

- Volumes are tied to a single host.
    
- No built-in way to manage persistent storage across nodes.
    

**Enterprise Impact:**

- If a container moves to another host, its data may be lost.
    
- Scaling stateful apps is error-prone.



## **What is an Ingress Controller?**

An **Ingress Controller** in Kubernetes is a component that:

- Watches **Ingress** resources in your cluster.
    
- Configures a **reverse proxy / load balancer** (like NGINX, Traefik, HAProxy) according to those rules.
    
- Routes **external traffic** (HTTP/HTTPS) to the correct internal services in your cluster.
    

Think of it as:

> The **doorman** to your Kubernetes building — it checks the guest list (Ingress rules) and sends visitors to the right room (service).

---

## **Why it’s Needed**

Without an Ingress Controller:

- Each service that needs public access would require its own **LoadBalancer** or **NodePort**.
    
- This can be costly and complex (especially in cloud environments where LoadBalancers cost money).
    

With an Ingress Controller:

- You can expose **multiple services** using **one public IP**.
    
- You can route based on **hostname** or **URL path**.


Imagine you have **three applications** running in Kubernetes:

| Domain           | Service Name | Purpose      |
| ---------------- | ------------ | ------------ |
| shop.example.com | shop-service | Online store |
| blog.example.com | blog-service | Company blog |
| example.com/api  | api-service  | Backend API  |
You only want **one IP address** and **one HTTPS certificate** for all of them.

## **Step 1: Deploy an Ingress Controller**

Example: Install NGINX Ingress Controller

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
`
This creates:

- The controller pods.
    
- A `LoadBalancer` service to accept external traffic.

## **Step 2: Create Ingress Rules**

Example **Ingress resource**:

`
`apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: shop.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: shop-service
            port:
              number: 80
  - host: blog.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: blog-service
            port:
              number: 80
  - host: example.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 80
`

## **Step 3: How Traffic Flows**

1. A user visits **https://shop.example.com**.
    
2. The DNS for `shop.example.com` points to the Ingress Controller’s public IP.
    
3. The Ingress Controller reads the rule:
    
    - `host: shop.example.com` → `shop-service:80`
        
4. The request is routed internally to the `shop-service` pods.
    

Same process works for `blog.example.com` and `example.com/api`.

## **Enterprise Benefits**

- **One point of entry** for all apps.
    
- **Centralized security**: TLS termination, authentication, rate limiting.
    
- **Cost savings**: One Load Balancer for many services.
    
- **Flexible routing**: Host-based and path-based rules.


**K8s Architecture**
![[maxresdefault.jpg]]

![[Kubernetes-architecture-968x1024.png]]


## **1. Our Design Goal**

When we started Kubernetes, our mission was clear:

> Build an **open, extensible, self-healing orchestration platform** that could run containers anywhere, scale to thousands of nodes, and survive failures without human babysitting.

We split it into **two main logical planes**:

- **Control Plane** → The _brain_ that makes all the decisions.
    
- **Worker Nodes** → The _muscle_ that actually runs your applications.
    

---

## **2. Control Plane Components (The Brain)**

### **a. kube-apiserver**

**Why**: We wanted a **single, well-defined API** that all clients and system components talk to.  
**What it does**:

- Accepts REST/gRPC requests (from `kubectl`, CI/CD pipelines, controllers).
    
- Validates and persists them in **etcd**.
    
- Acts as the “front desk” of Kubernetes.
    

**Example**:  
You run:
`kubectl apply -f shop-deployment.yaml
`
The API server:

1. Validates the YAML.
    
2. Stores the Deployment object in etcd.
    
3. Notifies the scheduler there’s work to do.
    

---

### **b. etcd**

**Why**: We needed a **distributed, strongly consistent key-value store** for cluster state.  
**What it does**:

- Stores _both_ desired state (configs, deployments) and observed state (which pods are actually running).
    
- Replicates across multiple control plane nodes for HA.
    

**Example**:  
When you define `replicas: 3` in your Deployment, that’s stored in etcd.  
If the cluster restarts, it reads from etcd to restore your app exactly as it was.

---

### **c. kube-scheduler**

**Why**: Someone needs to decide _where_ each pod runs.  
**What it does**:

- Watches for pods without a node assignment.
    
- Chooses the best node based on resource availability, affinities, taints/tolerations.
    

**Example**:  
Your `shop-service` needs 1 CPU and 2GB RAM — scheduler finds a node with available capacity and binds the pod there.

---

### **d. kube-controller-manager**

**Why**: We wanted a **loop-based control system** that constantly reconciles desired vs actual state.  
**What it does**:

- **ReplicaSet Controller** → Ensures the number of pods matches what you asked for.
    
- **Node Controller** → Watches node health, replaces workloads if a node dies.
    
- **Endpoints Controller** → Keeps service IPs updated with active pods.
    

**Example**:  
If one `shop-service` pod crashes, the ReplicaSet Controller immediately creates a new one — no human needed.

---

### **e. cloud-controller-manager**

**Why**: Enterprises needed to integrate with cloud provider features without hardcoding vendor logic.  
**What it does**:

- Talks to AWS, Azure, GCP APIs for load balancers, volumes, etc.
    

**Example**:  
When you create a `Service` of type `LoadBalancer`, it tells AWS/GCP/Azure to provision one and hook it into the cluster.

---

## **3. Worker Node Components (The Muscle)**

### **a. kubelet**

**Why**: Every node needed a local agent to carry out orders from the control plane.  
**What it does**:

- Talks to API server.
    
- Pulls container images via container runtime.
    
- Runs health checks.
    
- Sends pod status updates back to control plane.
    

**Example**:  
The scheduler says “Node 3 will run `shop-service` pod.”  
Kubelet on Node 3 pulls the image, runs the container, and confirms it’s healthy.

---

### **b. kube-proxy**

**Why**: We wanted built-in service discovery and load balancing between pods.  
**What it does**:

- Implements virtual IPs for Services.
    
- Routes requests to healthy pods behind a service.
    

**Example**:  
A user hits `shop.example.com`.  
kube-proxy ensures the request is sent to one of the active `shop-service` pods.

---

### **c. Container Runtime**

**Why**: Kubernetes itself doesn’t run containers — it delegates that.  
**What it does**:

- Pulls images from registries.
    
- Starts/stops containers.
    
- Manages container networking and storage.
    

**Example**:  
Could be **containerd**, **CRI-O**, or Docker (via shim).

---

## **4. Networking Model**

We made a bold choice:

- Every pod gets a **unique IP**.
    
- Flat, routable network — no NAT between pods.
    
- Services act as **stable endpoints**.
    

**Example**:  
The `shop-service` and `blog-service` can talk directly via pod IPs, without needing complex networking configs.

---

## **5. Real-Life Example Flow**

Let’s walk through **deploying an online store** inside Kubernetes:

1. **Developer** applies a YAML for `shop-service` with `replicas: 3`.
    
2. **API server** stores the deployment in **etcd**.
    
3. **Scheduler** picks 3 nodes for the pods.
    
4. **Kubelet** on each node starts a container from `shop:1.0` image.
    
5. **kube-proxy** routes traffic to these pods.
    
6. **Ingress Controller** (like NGINX) directs `shop.example.com` to `shop-service`.
    
7. If a node fails, **controller-manager** creates replacement pods on other nodes.


# **Deployment of app on k8s**

- Enable Kubernetes in Docker Desktop.
    
- Build the backend image locally.
    
- Create a small k8s manifest set (Namespace, Secret/ConfigMap, Deployment, Service).
    
- Deploy to the Docker Desktop k8s cluster.
    
- Expose/test (port-forward or Ingress).
    
- Optional: add a local Postgres (PVC), run migrations, debug, rollouts.
---
# 2) Prerequisites (check)

- Docker Desktop installed (you said yes).
    
- Kubernetes enabled in Docker Desktop (steps below).
    
- `kubectl` CLI available (Docker Desktop includes it; otherwise install it).
    
- (Optional) `helm` if you want to install ingress or other charts later.
    
- Ingress for custom domain routing
    
- Persistent volumes for DB

- service mesh
    
- Horizontal Pod Autoscaling
    
- Monitoring/logging
    
- CI/CD hooks
---

**Separate clusters** for dev, staging, and production.
Hosted Kubernetes service (EKS, GKE, AKS, OpenShift, etc.) for scalability and reliability.
**Multiple namespaces** per environment (e.g., `backend`, `frontend`, `monitoring`, `logging`).
**RBAC** (Role-Based Access Control) with least privilege access for teams and CI/CD.

---

# 3) Enable Kubernetes in Docker Desktop
Open Docker Desktop → Settings (Preferences) → **Kubernetes** → check **Enable Kubernetes** → Apply & Restart.
`kubectl version --client
`kubectl get nodes
 `you should see a node like "docker-desktop" and its STATUS should be Ready`

---
# 4) Build your backend container image (locally)
From your backend project root (where Dockerfile is:
`
`cd /path/to/your/backend
`docker build -t my-ecom-backend:dev . `
# verify image exists
`docker images | grep my-ecom-backend
`
**Notes**:  Docker Desktop’s k8s uses the same Docker daemon — local images are available to the cluster. To be safe in the manifests set `imagePullPolicy: IfNotPresent` (or `Never`) so k8s uses the local image.

---
# 5) Create a namespace (keeps things tidy)

`kubectl create namespace ecommerce
`

---
- **Namespace** → keeps your test resources grouped.
    
- **Secret/ConfigMap** → lets you inject configs without hardcoding.
    
- **Deployment** → actually runs your pods and handles restarts/upgrades.
    
- **Service** → exposes your pods internally (and externally if needed).

# **tear down & re-deploy**  
Testing on Docker Desktop means you’ll be redeploying a lot.wipe the whole thing instantly.
`kubectl delete ns ecommerce
`

# 6) Secrets / Config — create from CLI
 Create DB secrets or other sensitive vars
`kubectl create secret generic db-secret \
 `--from-literal=POSTGRES_PASSWORD='supersecret' \
 `--from-literal=POSTGRES_USER='postgres' \
 `-n ecommerce`
 
Create non-secret environment variables as a ConfigMap if needed:
`kubectl create configmap backend-config \
  `--from-literal=APP_ENV=development \
  `--from-literal=LOG_LEVEL=info \
  `-n ecommerce

# 7)  k8s manifests

# Namespace (optional if you already created it)
- **Multiple namespaces** per environment (e.g., `backend`, `frontend`, `monitoring`, `logging`).
apiVersion: v1
kind: Namespace
metadata:
  name: ecommerce
---
# Deployment for backend
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
  namespace: ecommerce
spec:
  replicas: 2
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
        - name: backend
          image: my-ecom-backend:dev
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8080
          envFrom:
            - configMapRef:
                name: backend-config
          env:
            - name: POSTGRES_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: db-secret
                  key: POSTGRES_PASSWORD
          readinessProbe:
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 15
            periodSeconds: 20
---
# Service exposing the backend internally
apiVersion: v1
kind: Service
metadata:
  name: backend-svc
  namespace: ecommerce
spec:
  type: ClusterIP
  selector:
    app: backend
  ports:
    - port: 80
      targetPort: 8080
---
# Optional Ingress (requires an Ingress Controller to be installed)
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: backend-ingress
  namespace: ecommerce
  annotations:
    kubernetes.io/ingress.class: "nginx"
spec:
  rules:
    - host: ecom.local
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: backend-svc
                port:
                  number: 80


# 8) Apply the manifests
`kubectl apply -f k8s/backend-all.yaml
`
# 9)Check status
`kubectl get all -n ecommerce`
`kubectl get pods -n ecommerce`
`kubectl rollout status deployment/backend -n ecommerce`

# 9) Access your app
