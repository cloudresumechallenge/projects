---
title: "Web App Deployment in kubernetes(K8s) Cluster"
---

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| E-commerce Web App Deployment in Kubernetes(K8s) Cluster | Google Cloud, AWS, Azure | This project highlights proficiency in Kubernetes and containerization, demonstrating the ability to deploy, scale, and manage web applications efficiently in a K8s environment, underscoring cloud-native deployment skills | [KodeKloud](https://kodekloud.com) |

## Intro

This version of the cloud resume challenge uses Kubernetes. Kubernetes is a popular (but advanced!) tool for orchestrating workloads in the cloud. If you're completely new to the cloud, consider doing one of the original Cloud Resume Challenge's before this one. The challenge covers the Kubernetes way of solving the following cloud challenges: 

- **Scalability:** How does an application adjust to fluctuating traffic?
- **Consistency:** How can you ensure an application is portable, and runs consistently in different environments?
- **Availability:** How can you update an application in production with zero downtime?

The Kubernetes Cloud Resume Challenge uses two key technologies: Docker and Kubernetes. Containerization with Docker encapsulates your application and its environment, ensuring it runs consistently. Kubernetes, a container orchestration platform, automates the deployment, scaling, and management by: 

- Adjusting application resources based on demand
- Restarting failed containers and reschedules them on healthy nodes.
- Configuration of zero-downtime updates and easy rollbacks.

> **Thank you!** - To the KodeKloud team for helping to put together these instructions. You can dive into [KodeKloud's Docker Learning Path](https://kodekloud.com/learning-path/docker/) and [Kubernetes Learning Path by KodeKloud](https://kodekloud.com/learning-path/kubernetes/) to master Kubernetes, enhance your project and preparing you for a future in cloud computing and DevOps.

## Prerequisites

The following steps will require the following knowledge and/or tools installed on your machine: 

- **Docker and Kubernetes CLI**: Required to build and pushing Docker images, and also manage Kubernetes resources.
- **Cloud Provider Account**: Access to AWS, Azure, or GCP for creating a Kubernetes cluster.
- **GitHub Account**: For version control and implementing CI/CD pipelines.

### Step 1: Certification

Complete the [Certified Kubernetes Application Developer (CKAD) course by KodeKloud](https://www.kodekloud.com/p/kubernetes-certification-course). 

**Outcome**: A CKAD certification. 

### Step 2: Containerize A Website

Kubernetes deploys applications packaged as containers. In this first step we'll create our container definitions for our workload.

- Create a Dockerfile with a running web application, exposed on port `80`

**Outcome**: A Dockerfile application. 

### Step 3: Containerize A Database

Most applications need some form of state in a database, let's configure one. 

- Instead of containerizing a database, grab an official database image. 
- Prepare a database initialization script to create any database schema.

**Outcome**: A database running in a docker container.

### Step 4: Push your containers to a registry

Push the created Docker image to a registry (e.g. DockerHub)

**Outcome**: Your application image stored in an image registry.

### Step 5: Set Up Kubernetes on a Public Cloud Provider


With your containers and Kubernetes configurations written, it's time to deploy them to the cloud. 

> **Note:** At this point you have a choice. You can use a tool like [MiniKube](https://minikube.sigs.k8s.io/) to experiment with your YAML configurations locally. Or, you can deploy a cluster in the cloud to test your configuration changes. 

- Choose AWS (EKS), Azure (AKS), or GCP (GKE) and follow their documentation to create a Kubernetes cluster. 
- Ensure you have `kubectl` configured to interact with your cluster.

**Outcome**: A deployed Kubernetes cluster.

### Step 6: Create your Kubernetes configurations

Kubernetes doesn't configure containers directly, but instead uses various "manifest" files and abstraction layers. 

- Create a Kubernetes [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) that references your Docker image in your registry
- Configure environment variables or mounts to allow your application to talk with your database.

**Outcome**: Your application is running on Kubernetes, with pods managed by the Deployment.

### Step 7: Create your Kubernetes service configuration

With only a deployment configuration, your application will not be accessible from the outside world at a stable URL. So, you'll need a [Service](https://kubernetes.io/docs/concepts/services-networking/service/). 

- Update your manifests to create a load balancer service. 

**Outcome**: An accessible URL or IP address for your web application.

### Step 8: Implement Configuration Management

With your app running, let's demonstrate how to configure your running application using a [ConfigMap](https://kubernetes.io/docs/concepts/configuration/configmap/). 

- Add a feature toggle to the web application to enable a "dark mode" for the website.

**Outcome**: Your website should now render in dark mode.

### Step 9: Scale Your Application

With your app running, you need to prepare for a marketing campaign and expect triple traffic. 

- Explore `kubectl` to run a command to manually scale the number of pods for your web application. 
- Once you've figured out how to scale manually, configure autoscaling. 

**Outcome**: The deployment automatically adjusts the number of pods based on CPU load, showcasing Kubernetes' capability to maintain performance under varying loads.

### Step 10: Rolling Update and Rollback

- Update the website to include a new promotional banner for the marketing campaign, apply the change using a rolling update. 
- Imagine the new banner you deployed introduced a bug. Roll back to the previous version.

**Outcome** Documented commands in a "runbook" (essentially, a document in your repo) that explains how to rollout and rollback your application. 

### Step 11: Implement Liveness and Readiness Probes

If your app becomes unresponsive, you want to ensure it is restarted. 

- Add, or re-use an endpoint (url) in your application to confirm it's operational status. 
- Ensure Kubernetes automatically restarts unresponsive pods and delays traffic to newly started pods until they're ready.

**Outcome** Defined probes for your application.

### Step 12: Utilize Secrets

Ensure you're not hardcoding any passwords or database strings in your application by using a Secret. 

- Reference your Secret in your manifest files / Deployment configuration. 

**Outcome** No hardcoded secrets in your repo, or manifest definitions. 

### Step 13: Document Your Process

1. **Finalize Your Project Code**: Ensure your project is complete and functioning as expected. Test all features locally and document all dependencies clearly.
2. **Create a Git Repository**: Create a new repository on your preferred git hosting service (e.g., GitHub, GitLab, Bitbucket).
3. **Push Your Code to the Remote Repository**
4. **Write Documentation**: Create a README.md or a blog post detailing each step, decisions made, and how challenges were overcome.

Add links to the Cloud Resume Challenge and KodeKloud sites as in the following.

- **Cloud Resume Challenge**: A hands-on project designed to deepen your understanding of cloud services through the practical application of building and deploying a resume. This challenge is an excellent way to apply what you've learned in a real-world scenario, enhancing your cloud skills. For more details, visit [Cloud Resume Challenge](https://cloudresumechallenge.dev/).

- **KodeKloud**: An interactive learning platform that offers a wide range of hands-on labs, courses, and real-world simulations tailored towards DevOps, Cloud, and software engineering practices. KodeKloud is an ideal resource for both beginners and experienced professionals looking to enhance their technical skills. Explore more at [KodeKloud](https://kodekloud.com/).

## Extra credit

### Package Everything in Helm

**Task**: Utilize Helm to package your application, making deployment and management on Kubernetes clusters more efficient and scalable.

1. **Create Helm Chart**: Start by creating a Helm chart for your application. This involves setting up a chart directory with the necessary templates for your Kubernetes resources.
2. **Define Values**: Customize your application deployment by defining variables in the `values.yaml` file. This allows for flexibility and reusability of your Helm chart across different environments or configurations.
3. **Package and Deploy**: Use Helm commands to package your application into a chart and deploy it to your Kubernetes cluster. Ensure to test your chart to verify that all components are correctly configured and working as expected.
4. **Outcome**: Your application is now packaged as a Helm chart, simplifying deployment processes and enabling easy versioning and rollback capabilities.

For more details, follow [KodeKloud Helm Course](https://kodekloud.com/courses/helm-for-beginners/).

### Implement Persistent Storage

**Task**: Ensure data persistence for the MariaDB database across pod restarts and redeployments.

1. **Create a PVC**: Define a PersistentVolumeClaim for MariaDB storage needs.
2. **Update MariaDB Deployment**: Modify the deployment to use the PVC for storing database data.
3. **Outcome**: Database data persists beyond the lifecycle of MariaDB pods, ensuring data durability.

### Implement Basic CI/CD Pipeline

**Task**: Automate the build and deployment process using GitHub Actions.

1. **GitHub Actions Workflow**: Create a `.github/workflows/deploy.yml` file to build the Docker image, push it to Docker Hub, and update the Kubernetes deployment upon push to the main branch.
2. **Outcome**: Changes to the application are automatically built and deployed, showcasing an efficient CI/CD pipeline.

## Appendix

The following are move advanced hints to the above instructions. Explore if you're stuck, but we recommend you use your initiative first. 

The below hints are based on: [kodekloudhub/learning-app-ecommerce](https://github.com/kodekloudhub/learning-app-ecommerce). 

### Containerizing

1. **Create a Dockerfile**: Navigate to the root of the e-commerce application and create a Dockerfile. This file should instruct Docker to:
   - Use `php:7.4-apache` as the base image.
   - Install `mysqli` extension for PHP.
   - Copy the application source code to `/var/www/html/`.
   - Update database connection strings to point to a Kubernetes service named `mysql-service`.
   - Expose port `80` to allow traffic to the web server.

2. **Build and Push the Docker Image**:
   - Execute `docker build -t yourdockerhubusername/ecom-web:v1 .` to build your image.
   - Push it to Docker Hub with `docker push yourdockerhubusername/ecom-web:v1`.
   - **Outcome**: Your web application Docker image is now available on Docker Hub.

### Configuration Management

1. **Modify the Web Application**: Add a simple feature toggle in the application code (e.g., an environment variable `FEATURE_DARK_MODE` that enables a CSS dark theme).
2. **Use ConfigMaps**: Create a ConfigMap named `feature-toggle-config` with the data `FEATURE_DARK_MODE=true`.
3. **Deploy ConfigMap**: Apply the ConfigMap to your Kubernetes cluster.
4. **Update Deployment**: Modify the `website-deployment.yaml` to include the environment variable from the ConfigMap.

### Scaling Manually

1. **Evaluate Current Load**: Use `kubectl get pods` to assess the current number of running pods.
2. **Scale Up**: Increase replicas in your deployment or use `kubectl scale deployment/ecom-web --replicas=6` to handle the increased load.
3. **Monitor Scaling**: Observe the deployment scaling up with `kubectl get pods`.
4. **Outcome**: The application scales up to handle increased traffic, showcasing Kubernetes' ability to manage application scalability dynamically.

#### Performing a Rolling Update

1. **Update Application**: Modify the web application's code to include the promotional banner.
2. **Build and Push New Image**: Build the updated Docker image as `yourdockerhubusername/ecom-web:v2` and push it to Docker Hub.
3. **Rolling Update**: Update `website-deployment.yaml` with the new image version and apply the changes.
4. **Monitor Update**: Use `kubectl rollout status deployment/ecom-web` to watch the rolling update process.

### Rolling Back a Deployment

1. **Identify Issue**: After deployment, monitoring tools indicate a problem affecting user experience.
2. **Roll Back**: Execute `kubectl rollout undo deployment/ecom-web` to revert to the previous deployment state.
3. **Verify Rollback**: Ensure the website returns to its pre-update state without the promotional banner.

### Autoscaling An Application

**Task**: Automate scaling based on CPU usage to handle unpredictable traffic spikes.

1. **Implement HPA**: Create a Horizontal Pod Autoscaler targeting 50% CPU utilization, with a minimum of 2 and a maximum of 10 pods.
2. **Apply HPA**: Execute `kubectl autoscale deployment ecom-web --cpu-percent=50 --min=2 --max=10`.
3. **Simulate Load**: Use a tool like Apache Bench to generate traffic and increase CPU load.
4. **Monitor Autoscaling**: Observe the HPA in action with `kubectl get hpa`.

### Liveness and Readiness Probes

1. **Define Probes**: Add liveness and readiness probes to `website-deployment.yaml`, targeting an endpoint in your application that confirms its operational status.
2. **Apply Changes**: Update your deployment with the new configuration.
3. **Test Probes**: Simulate failure scenarios (e.g., manually stopping the application) and observe Kubernetes' response.
