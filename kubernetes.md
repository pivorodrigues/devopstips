## Kubernetes - Company Course##
(Based on https://github.com/cezarsa/kube-intro-workshop)

#

**Kubernetes Intro**

**What is Kubernetes?**

- "Kubernetes is a container orchestrator. But, not only a container orchestrator"

  **It knows:**

  **How** to start containers
  **When** to start containers
  **Where** to start containers

  It keeps trying to change the real world (nodes, containers, networks) to make it match a set of definitions.
  It never stops trying as external factors can change the real world state at any time.

#

**Concepts**

- Kubernetes provides an API for CRUDing objects.

  - Basic objects:

    - Pods
    - Namespaces
    - Services
    - Endpoints
    - Volumes
    - Nodes

  The control plane is responsible for storing these objects and doing something with them.

  Kubectl is a CLI that can talk to the Kubernetes API in a user friendly way.

- **YAML Example:**

  ```
  apiVersion: v1
  kind: Pod

  metadata:
    name: mypod
    labels:
    annotations:

  spec:
    containers:
      - name: mypod1
        image: busybox

  status:
  ```

#

$ kubectl get pod mypod -o wide

$ kubectl describe pod <pod name>
