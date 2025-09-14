# Kubernetes Python App - Scalable and Fault-tolerant.

A simple Python Flask API deployed using Docker and Kubernetes (Minikube), demonstrating scalable, fault-tolerant web service architecture.

## Project Setup
<p align="center">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="Python" width="40"/>
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/flask/flask-original.svg" alt="Flask" width="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original.svg" alt="Docker" width="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/kubernetes/kubernetes-plain.svg" alt="Kubernetes" width="40"/>
  <img src="https://www.svgrepo.com/show/373297/minikube-opened.svg" alt="Minikube" width="40"/>
</p>

### Prerequisites

- Python 3.11+
- Docker
- Minikube (for local Kubernetes)
- kubectl (configured with Minikube)

### 1. Clone and Build

```
git clone https://github.com/aashishmalviya/kubernetes_smol.git
cd kubernetes_smol
eval $(minikube docker-env)
docker build -t flask-hello:latest .
```

### 2. Deploy to Kubernetes

Apply the deployment and service manifests:

```
kubectl apply -f k8s-deployment.yaml
kubectl apply -f k8s-service.yaml
```

### 3. Access the App

Query the app from your browser or CLI:

```
minikube service flask-hello-service
```
or

```
curl $(minikube ip):30007
```

## 4. Fault Tolerance

- Multiple replicas (configure in `k8s-deployment.yaml`) ensure your app service remains available if any pod fails.
- Kubernetes continually monitors pods; if a pod fails/crashes, it automatically starts a replacement to maintain the desired replica count.
- Incoming requests are load-balanced across all running pods via the service abstraction.

## How to Test Fault Tolerance

1. **Increase Replicas**
    ```
    Edit k8s-deployment.yaml and set replicas to your desired number (e.g., 5).
    ```
    Or run:
    ```
    kubectl scale deployment flask-hello-deployment --replicas=5
    ```

2. **Simulate Failure**

    Manually delete pods:

    ```
    kubectl get pods -l app=flask-hello
    kubectl delete pod <pod-name>
    ```

    Kubernetes will immediately create new pods to restore replica count -> demonstrating automatic self-healing and availability.

3. **Verify**

    Refresh `kubectl get pods` to watch recovery. The exposed service remains continuously available for requests.

## Tech Stack

| Technology       | Purpose                                       |
|------------------|-----------------------------------------------|
| Python           | Application language (Flask API)              |
| Flask            | Web framework for REST API                    |
| Docker           | Containerizing the Python app                 |
| Kubernetes       | Orchestrating, scaling, and self-healing app  |
| Minikube         | Local Kubernetes cluster                      |
| kubectl          | Command-line control for Kubernetes           |

<br>
<p align="center">
  Like it? ❤️ <a href="https://linkedin.com/in/aashish-malviya">Let's connect 🤗</a>
</p>