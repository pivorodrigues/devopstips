## <img src="images/rancher.png" width="50px"> Rancher Certification Notes <img src="images/rancher.png" width="50px">

### Week 1: Intro to Rancher and RKE

### 1.1. Learning the Rancher Architecture

- **1.1.2: Communication With Downstream Clusters**

    - **Authentication Proxy**

        - Receives requests from a user

        - Authenticates the user  

        - Forwards request to Kubernetes on behalf of user

    - **Authentication**

        - Who are you?

        - Handled by Rancher

    - **Authorization**

        - What are you allowed to do?

        - Handled by Kubernetes

    - **Cluster Controller**

        - Runs within Rancher cluster

        - One per Kubernetes cluster

        - Watches for resource changes

        - Controls downstream cluster state

        - Configures access control policies

        - Provisions clusters

    - **Cluster Agent**

        - Connects to Kubernetes API

        - Manages workloads within each cluster

        - Applying roles and bindings

        - Communicates w/ Rancher server through tunnel

    - **Node Agent**
    
        - Runs as a DaemonSet

        - Upgrades Kubernetes

        - Restores etcd snapshots

        - Can fill in for Cluster Agent

    - **Authorized Cluster Endpoint**

        - Enables direct communication

        - Useful if Rancher is down

        - Enables direct communication

        - Useful if cluster is closer to user than Rancher