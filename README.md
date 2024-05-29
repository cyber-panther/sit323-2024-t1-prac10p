# README - SIT323 Task 10.1P

This task demonstrated the implementation of monitoring and visibility for a cloud-native application using Google Cloud Platform (GCP) tools. The application was containerized using Node.js, Docker, and Kubernetes, and deployed to a GCP Kubernetes cluster. GCP tools were then used to collect and analyze metrics and logs from the application and the Kubernetes cluster.

### 1. Build the Docker Image

The Docker image for the Node.js application was built with the following command:

```bash
docker build -t agrimgautam/sit323-2024-t1-prac5p:latest .
```

### 2. Push the Docker Image to Docker Hub

The Docker image was pushed to Docker Hub with this command:

```bash
docker push agrimgautam/sit323-2024-t1-prac5p:latest
```

### 3. Create a GKE Cluster

A cluster consisting of at least one cluster control plane machine and multiple worker machines called nodes was created. Nodes are Compute Engine virtual machine (VM) instances that run the Kubernetes processes necessary to make them part of the cluster. Applications were deployed to clusters, and the applications ran on the nodes.

An Autopilot cluster named `sit323-cluster` was created with this command:

```bash
gcloud container clusters create-auto sit323-cluster \
    --location=us-central1
```

### 4. Get Authentication Credentials for the Cluster

After creating the cluster, authentication credentials were obtained to interact with the cluster:

```bash
gcloud container clusters get-credentials sit323-cluster \
    --location us-central1
```

This command configured `kubectl` to use the created cluster.

### 5. Deploy the Application to the Cluster

After the cluster was created, the containerized application was deployed to it.

#### Create the Deployment

The application was deployed to the cluster by running the following command:

```bash
kubectl create deployment sit323-server \
    --image=agrimgautam/sit323-2024-t1-prac5p:latest
```

This Kubernetes command, `kubectl create deployment`, created a Deployment named `sit323-server`. The Deployment's Pod ran the `sit323-app` container image.

#### Expose the Deployment

To expose the application, the following `kubectl expose` command was used:

```bash
kubectl expose deployment sit323-server \
    --type LoadBalancer \
    --port 80 \
    --target-port 3000
```

### 6. Inspect and View the Application

The running Pods were inspected using `kubectl get pods`:

```bash
kubectl get pods
```

This command confirmed that one `sit323-server` Pod was running on the cluster.

The `sit323-server` Service was inspected using `kubectl get service`:

```bash
kubectl get service sit323-server
```

The application was then viewed from a web browser using the external IP address with the exposed port:

```http://EXTERNAL_IP```

This completed the deployment of a containerized web application to GKE.

## Suggestions for Screenshots

1. **GKE Cluster Creation:** Screenshot of the GCP Console showing the creation of the GKE cluster `sit323-cluster`.
2. **Docker Hub:** Screenshot of the Docker Hub repository showing the pushed image `agrimgautam/sit323-2024-t1-prac5p:latest`.
3. **Kubernetes Deployment:** Screenshot of the Kubernetes dashboard showing the `sit323-server` deployment.
4. **Service Exposure:** Screenshot of the GCP Console or `kubectl get services` command showing the exposed service with the external IP.
5. **Stackdriver Monitoring Dashboard:** Screenshot of the Stackdriver Monitoring dashboard with relevant metrics.
6. **Stackdriver Logging:** Screenshot of the Stackdriver Logging console showing logs from the `sit323-server`.

Ensure to capture these screenshots during your implementation process to include them in your final report.