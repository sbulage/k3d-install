![k3d_logo_black_blue](https://user-images.githubusercontent.com/12134754/229094385-1b01f89e-ba99-471e-8534-b3bea4d4e77a.svg)

---
# What is k3d?

- k3d is a lightweight wrapper to run [K3s](https://docs.k3s.io/) (Rancher Lab’s minimal Kubernetes distribution) in docker.

- k3d makes it very easy to create single- and multi-node k3s clusters in docker, e.g. for local development on Kubernetes.

For information read it here: [k3d](https://k3d.io/v5.4.9/)

---

# Install K3d

## Pre-requisites:

- Docker is must to install/interact with K3d.

- Download [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)


---

### Virtual Machines configuration used in this guide.

- 1 VM with 4 CPU and 8GB Ram

---

## Let's begin with Installation and Setup.

Initially we will install the Docker in the system.(Skip this step if Docker is already present in the system)

### Docker Installation

- Install Docker and Check it's running in the system.

        sudo zypper install docker

- Start the docker daemon during boot:

        sudo systemctl enable docker

- Join the docker group that is allowed to use the docker daemon:

        sudo usermod -G docker -a $USER

- Restart the docker daemon:

        sudo systemctl restart docker

- Verify docker is running:

        docker version

### k3d Installation

- There are 2 ways you can fetch the k3d binary -- cURL or wget comamnd as below.

    - cURL:

            curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

    - wget:

            wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

- Let's see the ***k3d*** options

        $ k3d --help
        https://k3d.io/
        k3d is a wrapper CLI that helps you to easily create k3s clusters inside docker.
        Nodes of a k3d cluster are docker containers running a k3s image.
        All Nodes of a k3d cluster are part of the same docker network.

        Usage:
          k3d [flags]
          k3d [command]

        Available Commands:
          cluster      Manage cluster(s)
          completion   Generate completion scripts for [bash, zsh, fish, powershell | psh]
          config       Work with config file(s)
          help         Help about any command
          image        Handle container images.
          kubeconfig   Manage kubeconfig(s)
          node         Manage node(s)
          registry     Manage registry/registries
          version      Show k3d and default k3s version

        Flags:
          -h, --help         help for k3d
              --timestamps   Enable Log timestamps
              --trace        Enable super verbose output (trace logging)
              --verbose      Enable verbose output (debug logging)
              --version      Show k3d and default k3s version

        Use "k3d [command] --help" for more information about a command.

- Create our new cluster

        k3d cluster create mycluster   #Cluster name used in this example.

- Check cluster is up and running

        k3d cluster list

- Start the cluster

        k3d cluster start mycluster   # Cluster name

- Try to access the cluster

        kubectl get nodes

- Locate ***kubeconfig*** file

        k3d kubeconfig get >> mykubeconfig
        or 
        k3d kubeconfig merge <PATH>         # Path where you wanted to save file.

- Stop cluster

        k3d cluster stop mycluster     # Cluster name

- Delete cluster

        k3d cluster delete mycluster   # Cluster name
--- 
Now play with the k3d and create as many clusters as you want. But make sure you delete the clusters once their used is over to save resources(and cost if machines running in cloud.)

## Stay Connected and do check other posts on my GH dashboard [sbulage](https://github.com/sbulage)
