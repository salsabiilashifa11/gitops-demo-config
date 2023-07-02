# gitops-demo-config

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#tech-stack">Tech Stack</a></li>
        <li><a href="#concepts-and-architecture">Concepts and Architecture</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>


<!-- ABOUT THE PROJECT -->
## About the Project

<!-- Tech Stack -->
### Tech Stack

<!-- Concepts and Architecture -->
### Concepts and Architecture

<!-- GETTING STARTED -->
## Getting Started

<!-- Prerequisites -->
### Prerequisites

<!-- Installation -->
### Installation
#### 1. Setup Kubernetes Cluster
This demo will deploy our application to a Kubernetes cluster. So let's get one up and running. Any form of Kubernetes cluster will work, self-managed, cloud-managed, or in this case, a light-version local cluster that will be created using Minikube. 

```
minikube start --memory=4096 --driver=docker
```

This will spin up a kubernetes cluster with Docker as the hypervisor and it will be given a memory of 4GB. You can choose different driver and memory settings if you will, or just remove them if you opt to use default settings. 

#### 2. Install ArgoCD
Next, you will need to install ArgoCD in your cluster, which you can do by running the following commands:

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

#### 3. Accessing ArgoCD using Web UI
You can monitor ArgoCD from its web interface. In order to do that, you can expose the server as an external LoadBalancer, or use port forwarding. 
In this demo, we opt to use port-forwarding, as we deal with Minikube. 

```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Get the default password from the secret with the name: `argocd-initial-admin-secret`, or use the following command.
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Access the web on `https://localhost:8080`

<!-- Acknowledgements -->
### Acknowledgements
