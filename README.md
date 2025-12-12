<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Deliverable 5 – Kubernetes Deployment using Minikube</title>
</head>
<body>

<h1>Deliverable 5 – Kubernetes Deployment using Minikube</h1>

<p>This repository contains the complete implementation for <strong>Deliverable 5</strong> — deploying a Dockerized Node.js application to a <strong>Minikube Kubernetes cluster</strong>.</p>

<hr>

<h2>Project Overview</h2>
<p>The application is a simple Node.js API that shows the available endpoints in JSON format:</p>

<pre><code>{"endpoints":["/ping","/current-date","/fibo/:n"]}</code></pre>

<ul>
  <li><strong>/ping</strong> → Check if the server is live</li>
  <li><strong>/current-date</strong> → Returns the current server date</li>
  <li><strong>/fibo/:n</strong> → Calculates the nth Fibonacci number</li>
</ul>

<p>This project demonstrates:</p>
<ul>
  <li>Dockerizing a Node.js app</li>
  <li>Pushing the Docker image to Docker Hub</li>
  <li>Creating Kubernetes Deployment & Service manifests</li>
  <li>Deploying the app on Minikube</li>
  <li>Accessing the app via NodePort</li>
</ul>

<hr>

<h2>Folder Structure</h2>
<pre><code>
deliverable5-minikube/
├── app.js
├── Dockerfile
├── package.json
├── package-lock.json
├── README.md
└── k8s/
    ├── deployment.yml
    └── service.yml
</code></pre>

<hr>

<h2>Docker Hub Image</h2>
<p>The Docker image used in Kubernetes deployment:</p>
<pre><code>docker.io/jaweriyakhan/sample-app:latest</code></pre>

---

<h2>Part A – Minikube & Environment Setup</h2>
<h3>1. Start Minikube</h3>
<pre><code>minikube start --driver=docker</code></pre>

<h3>2. Verify Cluster</h3>
<pre><code>kubectl get nodes
kubectl get pods -A</code></pre>

<p><em>Screenshot placeholder: Insert screenshot showing nodes and system pods running</em></p>

<hr>

<h2>Part B – Kubernetes Deployment Files</h2>

<h3>Deployment (k8s/deployment.yml)</h3>
<pre><code>apiVersion: apps/v1
kind: Deployment
metadata:
  name: sample-app-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: sample-app
  template:
    metadata:
      labels:
        app: sample-app
    spec:
      containers:
      - name: sample-app-container
        image: jaweriyakhan/sample-app:latest
        ports:
        - containerPort: 3000</code></pre>

<h3>Service (k8s/service.yml)</h3>
<pre><code>apiVersion: v1
kind: Service
metadata:
  name: sample-app-service
spec:
  type: NodePort
  selector:
    app: sample-app
  ports:
  - port: 3000
    targetPort: 3000
    nodePort: 30100</code></pre>

<hr>

<h2>Part C – Deploy to Minikube</h2>

<h3>1. Apply manifests</h3>
<pre><code>kubectl apply -f k8s/deployment.yml
kubectl apply -f k8s/service.yml</code></pre>

<h3>2. Verify pods</h3>
<pre><code>kubectl get pods</code></pre>
<p><em>Screenshot placeholder: Insert screenshot showing pods running (1/1)</em></p>

<h3>3. Open app in browser</h3>
<pre><code>minikube service sample-app-service</code></pre>
<p><em>Screenshot placeholder: Insert screenshot of browser showing JSON endpoints</em></p>

<hr>

<h2>Testing Endpoints</h2>
<ul>
  <li><strong>/ping</strong></li>
  <li><strong>/current-date</strong></li>
  <li><strong>/fibo/:n</strong></li>
</ul>
<p>Example:</p>
<pre><code>http://&lt;minikube-service-url&gt;/fibo/10</code></pre>

<hr>

<h2>Submission Checklist</h2>
<ul class="checklist">
  <li>Minikube installed & running</li>
  <li>Docker image pushed to Docker Hub</li>
  <li>Kubernetes Deployment + Service created</li>
  <li>App accessible in browser</li>
  <li>Screenshots captured</li>
  <li>README.md included</li>
</ul>

<hr>

<h2>Conclusion</h2>
<p>This completes <strong>Deliverable 5</strong> — demonstrating container orchestration using Minikube, Docker, and Kubernetes with a working Node.js application.</p>

</body>
</html>
