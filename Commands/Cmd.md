# Kubernetes `kubectl` Full Reference (v1.32 / v1.33‑style)

> **Syntax**  
> `kubectl [command] [TYPE] [NAME] [flags]` :contentReference[oaicite:0]{index=0}

---

## Table of Contents

1. Global/Common Options  
2. Main Commands  
   1. Basic Resource Management  
   2. Scale / Rollout / Set / Expose / Run etc.  
   3. Cluster / Namespace / Context etc  
   4. Debug / Port‑forward / Logs etc  
   5. Others: api‑resources, top, plugin, etc  
3. Flags by Command (major ones)  
4. Examples

---

## 1. Global / Common Options (for many commands)

These are flags that apply to many `kubectl` commands (inherited flags). :contentReference[oaicite:1]{index=1}

| Flag | Shorthand | Default / Value Type | Description |
|---|---|---|---|
| `--as string` | — | string | Impersonate as given user. :contentReference[oaicite:2]{index=2} |
| `--as-group strings` | — | list of groups | Impersonate as given group(s). :contentReference[oaicite:3]{index=3} |
| `--as-uid string` | — | string | Impersonate as given UID. :contentReference[oaicite:4]{index=4} |
| `--certificate-authority string` | — | path | Path to a cert file for the authority. :contentReference[oaicite:5]{index=5} |
| `--client-certificate string` | — | path | TLS client certificate file. :contentReference[oaicite:6]{index=6} |
| `--client-key string` | — | path | TLS client key file. :contentReference[oaicite:7]{index=7} |
| `--cluster string` | — | name | Which cluster in kubeconfig to use. :contentReference[oaicite:8]{index=8} |
| `--context string` | — | name | Which context in kubeconfig to use. :contentReference[oaicite:9]{index=9} |
| `--kubeconfig string` | — | path | Path to the kubeconfig file. (Often global) |
| `--namespace, -n string` | `-n` | string (namespace) | Namespace to use for the command. :contentReference[oaicite:10]{index=10} |
| `--user string` | — | string | Which user to use from kubeconfig. |
| `--output, -o string` | `-o` | formats (json, yaml, name, wide, etc) | Output format. :contentReference[oaicite:11]{index=11} |
| `--dry-run=(none\|server\|client)` | — | one of none/server/client | Do not persist resource; simulate. :contentReference[oaicite:12]{index=12} |
| `--save-config` | — | bool | If true, records the configuration of the current object in its annotation; useful for future `apply`. :contentReference[oaicite:13]{index=13} |
| `--validate` | — | bool | Validate input against the schema before sending to server. :contentReference[oaicite:14]{index=14} |
| `--field-manager string` | — | string | Name of the manager used to track ownership of fields. :contentReference[oaicite:15]{index=15} |
| `--allow-missing-template-keys` | — | bool | Ignore errors in templates if a field or map key is missing. :contentReference[oaicite:16]{index=16} |

---

## 2. Main Commands

Here is a list of the main `kubectl` commands, with their purposes and major flags.

---

### 2.1 Basic Resource Management

| Command | Description |
|---|---|
| `kubectl create` | Create a resource from YAML/JSON file or direct arguments. :contentReference[oaicite:17]{index=17} |
| `kubectl get` | List one or more resources. Can use `-o` to select output format, selectors, etc. :contentReference[oaicite:18]{index=18} |
| `kubectl describe` | Show details of a specific resource. :contentReference[oaicite:19]{index=19} |
| `kubectl delete` | Delete resources by name, file, or selector. :contentReference[oaicite:20]{index=20} |
| `kubectl apply` | Create or update resources from a file or directory (idempotent). |

---

### 2.2 Scale / Rollout / Set / Expose / Run / Autoscale

| Command | Description |
|---|---|
| `kubectl scale` | Change the number of replicas for a resource (deployment, statefulset etc). |
| `kubectl rollout` | Manage the rollout of deployments (pause, resume, undo, history). :contentReference[oaicite:21]{index=21} |
| `kubectl set` | Set specific features on objects, e.g. images, resources requests/limits. |
| `kubectl expose` | Expose a resource (deployment, pod etc) as a service. |
| `kubectl run` | Run a new pod or deployment with specified image; useful for simple / testing workloads. |
| `kubectl autoscale` | Automatically scale resource (deployment, etc) based on metrics. |

---

### 2.3 Cluster / Namespace / Context etc.

| Command | Description |
|---|---|
| `kubectl config` | Modify kubeconfig: contexts, clusters, credentials. |
| `kubectl cluster-info` | Display cluster info (master, services). |
| `kubectl namespace` | Manage namespaces (create, delete etc). Often via `kubectl create namespace …`. |

---

### 2.4 Debug / Logs / Port / Exec etc.

| Command | Description |
|---|---|
| `kubectl logs` | Print logs for a pod / container. |
| `kubectl exec` | Execute a command in a container in a pod. |
| `kubectl port-forward` | Forward local port to a pod. |
| `kubectl cp` | Copy files or directories to/from a pod. |
| `kubectl attach` | Attach to a running container. |
| `kubectl debug` | Create debugging containers, etc. |

---

### 2.5 Info / Tools / Other

| Command | Description |
|---|---|
| `kubectl api-resources` | List the API resources supported by the cluster. :contentReference[oaicite:22]{index=22} |
| `kubectl api-versions` | List the supported API versions. |
| `kubectl version` | Print client and server version. |
| `kubectl top` | Display resource usage (CPU / memory) for nodes or pods. |
| `kubectl explain` | Get documentation for a resource (fields, etc). |
| `kubectl plugin` | Manage or call external plugins. |
| `kubectl help` | Show the help for commands / get usage. |

---

## 3. Flags by Some Key Commands

Here are some major flags specific to particular commands (not global), for important commands.

---

### `kubectl get`

| Flag | Shorthand | Description |
|---|---|---|
| `-o, --output` | `-o` | json, yaml, wide, name etc. |
| `--template` / `--templatefile` | — | Use Go templates to format output. |
| `-w, --watch` | `-w` | Watch for changes. |
| `--field-selector` | — | Filter by resource fields. |
| `-l, --selector` | `-l` | Filter by labels. |
| `--all-namespaces, -A` | `-A` | Across all namespaces. |

---

### `kubectl create`

| Flag | Description |
|---|---|
| `--image` | Specify image for deployments/pods etc. |
| `--replicas` | Number of replicas. |
| `--schedule` | For cronjob. |
| `--command -- [COMMAND args]` | Execute specific command in the container. |
| `--dry-run` | Simulate without persisting. |

---

### `kubectl apply`

| Flag | Description |
|---|---|
| `-f, --filename` | Filename, directory or URL to manifest files. |
| `--recursive, -R` | Process directories recursively. |
| `--prune` | Remove objects that are not in the manifest. |
| `--server-side` | Apply changes server‑side. |

---

### `kubectl rollout`

| Sub‑command | Description |
|---|---|
| `kubectl rollout status <resource>` | Show rollout status. |
| `kubectl rollout history <resource>` | Show rollout history. |
| `kubectl rollout undo <resource>` | Rollback to previous. |
| `kubectl rollout pause/resume <resource>` | Pause/resume deployments. |

---

### `kubectl set`

| Sub‑command | Description |
|---|---|
| `kubectl set image` | Change image of container(s). |
| `kubectl set resources` | Set CPU / memory requests & limits. |
| `kubectl set selector` | Change labels/selectors. |
| `kubectl set env` | Set environment variables. |

---

## 4. Examples

Here are some example usages to illustrate combining commands + flags.

```bash
# Get all pods in all namespaces, wide output:
kubectl get pods --all-namespaces -o wide

# Create deployment with 3 replicas
kubectl create deployment nginx --image=nginx --replicas=3

# Expose deployment as service
kubectl expose deployment nginx --port=80 --type=LoadBalancer

# Update image via set
kubectl set image deployment/nginx nginx=nginx:1.21

# Rollout history and rollback
kubectl rollout history deployment/nginx
kubectl rollout undo deployment/nginx

# Port-forward to a pod
kubectl port-forward pod/nginx-pod 8080:80

# Debug
kubectl debug pod/nginx-pod --image=busybox -- /bin/sh

# Check resource usage
kubectl top pod nginx-pod
kubectl top node
