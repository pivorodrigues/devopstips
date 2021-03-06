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

- **1.1.3 - Architectural Best Practices**

    - Run a Docker deployment of Rancher on its own node (If you are using a Docker version of Rancher)

    - Run it on a separate node from all Kubernetes workloads

    - Don't run it on the same node as the Kubernetes cluster is managing

    - Run a Kubernetes deployment of Rancher in an RKE cluster

    - Dedicate that cluster to Rancher

    - If Rancher is managing production workloads, run an HA Rancher cluster

    - Use a layer 4 load balancer in front of HA Rancher cluster

    - Avoid doing SSL termination on the load balancer

    - Run the Rancher cluster near the downstream clusters it's managing

    - The Rancher management cluster can start with three nodes and add aditional workers as it grows

    - Downstream clusters can combine or split etcd and controlplane roles

    - Put a layer 4 load balancer in front of the controlplane nodes when using the Authorized Cluster Endpoint Feature

    - Watch the Rancher management cluster. As you add more downstream clusters, it will need to grow to handle them.

#

### 1.2. Discovering RKE

- **1.2 - Introduction**

  - Minimal **cluster.yml** example:

    ```
        nodes:
            - address: 1.2.3.4
              user: ubuntu
              role:
                - controlplane
                - etcd
                - worker  
    ```

  - **RKE Configuration**

    - Declarative configuration file

    - Apply it with **"rke up"**

    - Runs from a local workstation

    - Connects over SSH

    - Installs Kubernetes

    - Generates a kubectl config

    - Changes happen in config file

    - Changes ar applied with **"rke up"**

- **1.2.1 - Installing RKE**

    - **Installing RKE**

      - Download the binary (https://github.com/rancher/rke)  

      - Move it into your path (`/usr/bin/rke`)

      - Make it executable (`#chmod +x /usr/bin/rke`)

- **1.2.2 - Preparing Nodes for Kubernetes**

    - **Node Preparation**

      1. SSH user in docker group

      2. Disable swap on workers

      3. Supported Versions (https://rancher.com/support-maintenance-terms)

      4. Installing Docker (https://rancher.com/docs/rancher/v2.x/en/installation/resources/installing-docker/)

    - **SSH Configuration (Server)**

      - `AllowTcpForwarding yes`

      - Your public key in `authorized_keys`

    - **SSH Configuration (Client)**

      - Use `--ssh-agent-auth` if your key has a passphrase

- **1.2.3. Creating the Cluster Configuration File**

    - Minimal RKE Configuration           

      ```
        nodes:
          - address: 192.168.100.101
          user: ubuntu
          role:
            - controlplane
            - etcd
            - worker
      ```    

    - **Generating the Config**

      - Use "rke config"

      - Answer questions

      - Customize the config

- **1.2.4. Certificate Options**

  - Kubernetes uses TLS certificates (also called SSL certificates) to secure communication between you and the cluster and between the cluster components.

  - Kubernetes secures communication between its nodes with TLS certificates. These certificates don't have to be certificates signed by a public CA, and by default RKE auto-generates the certificates for you.

  - If you would prefer to use your own certificates, you can either use a custom certificate directory that has your certs in it, or you can have RKE generate CSRs to be signed by an external CA. They'll have all of the correct Alternative DNS and IP names for the cluster.

  - Once you receive signed certificates from the CA, you can use them as custom certificates.