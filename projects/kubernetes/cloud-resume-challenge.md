---
title: "Web App Deployment in kubernetes(K8s) Cluster"
---

| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| E-commerce Web App Deployment in Kubernetes(K8s) Cluster | Google Cloud, AWS, Azure | This project highlights proficiency in Kubernetes and containerization, demonstrating the ability to deploy, scale, and manage web applications efficiently in a K8s environment, underscoring cloud-native deployment skills | [KodeKloud](https://kodekloud.com) |

## Intro

Imagine you are going to deploy an e-commerce website, it's crucial to consider the challenges of modern web application deployment and how containerization and Kubernetes (K8s) offer compelling solutions:

- **Scalability:** How can your application automatically adjust to fluctuating traffic?
- **Consistency:** How do you ensure your application runs the same across all environments?
- **Availability:** How can you update your application with zero downtime?

Containerization, using Docker, encapsulates your application and its environment, ensuring it runs consistently everywhere. Kubernetes, a container orchestration platform, automates deployment, scaling, and management, offering:

- **Dynamic Scaling:** Adjusts application resources based on demand.
- **Self-healing:** Restarts failed containers and reschedules them on healthy nodes.
- **Seamless Updates & Rollbacks:** Enables zero-downtime updates and easy rollbacks.

By leveraging Kubernetes and containerization for your Cloud Resume Challenge, you embrace a scalable, consistent, and resilient deployment strategy. This not only demonstrates your technical acumen but aligns with modern DevOps practices.

Dive into [KodeKloud's Docker Learning Path](https://kodekloud.com/learning-path/docker/) and [Kubernetes Learning Path by KodeKloud](https://kodekloud.com/learning-path/kubernetes/) to master these technologies, enhancing your project and preparing you for a future in cloud computing and DevOps.


## Challenge Guide

### Prerequisites

Before you embark on this journey, ensure you are equipped with:

- **Docker and Kubernetes CLI Tools**: Essential for building, pushing Docker images, and managing Kubernetes resources.
- **Cloud Provider Account**: Access to AWS, Azure, or GCP for creating a Kubernetes cluster.
- **GitHub Account**: For version control and implementing CI/CD pipelines.
- **E-commerce Application Source Code and DB Scripts**: Available at [kodekloudhub/learning-app-ecommerce](https://github.com/kodekloudhub/learning-app-ecommerce). Familiarize yourself with the application structure and database scripts provided.

## Step-by-Step Implementation

### Step 1: Certification

**KodeKloud CKAD Course**: To ensure you have a solid understanding of Kubernetes concepts and practical experience, complete the [Certified Kubernetes Application Developer (CKAD) course by KodeKloud](https://www.kodekloud.com/p/kubernetes-certification-course). This course will equip you with the knowledge and skills needed to tackle this challenge effectively.

### Step 2: Containerizing Your E-Commerce Website and Database

#### A. Web Application Containerization

##### 1. Creating a Dockerfile
- This Dockerfile should base itself on a specific web server image. It must include necessary extensions, your application's source code, configurations for database connections to align with a named Kubernetes service, and the port the web server listens on for web traffic.

##### 2. Building and Pushing Docker Image
- Use the Dockerfile to build your web application's image. Then, push this image to a container registry, such as Docker Hub, to make it distributable.

#### B. Database Containerization
- Choose an official database image that fits your e-commerce site's requirements. Prepare any necessary database initialization scripts that are compatible with container orchestration services (like Kubernetes) for the initial setup.

### Step 3: Set Up Kubernetes on a Public Cloud Provider

- **Cluster Creation**: Choose AWS (EKS), Azure (AKS), or GCP (GKE) and follow their documentation to create a Kubernetes cluster. Ensure you have `kubectl` configured to interact with your cluster.
- **Outcome**: A fully operational Kubernetes cluster ready for deployment.

### Step 4: Deploy Your Website to Kubernetes

- **Kubernetes Deployment**: Create a `website-deployment.yaml` defining a Deployment that uses the Docker image created in Step 1A. Ensure the Deployment specifies the necessary environment variables and mounts for the database connection.
- **Outcome**: The e-commerce web application is running on Kubernetes, with pods managed by the Deployment.

### Step 5: Expose Your Website

- **Service Creation**: Define a `website-service.yaml` to create a Service of type `LoadBalancer`. This Service exposes your Deployment to the internet.
- **Outcome**: An accessible URL or IP address for your web application.

### Step 6: Implement Configuration Management

**Task**: Add a feature toggle to the web application to enable a "dark mode" for the website.

1. **Modify the Web Application**: Add a simple feature toggle in the application code (e.g., an environment variable `FEATURE_DARK_MODE` that enables a CSS dark theme).
2. **Use ConfigMaps**: Create a ConfigMap named `feature-toggle-config` with the data `FEATURE_DARK_MODE=true`.
3. **Deploy ConfigMap**: Apply the ConfigMap to your Kubernetes cluster.
4. **Update Deployment**: Modify the `website-deployment.yaml` to include the environment variable from the ConfigMap.
5. **Outcome**: Your website should now render in dark mode, demonstrating how ConfigMaps manage application features.

### Step 7: Scale Your Application

**Task**: Prepare for a marketing campaign expected to triple traffic.

1. **Evaluate Current Load**: Use `kubectl get pods` to assess the current number of running pods.
2. **Scale Up**: Increase replicas in your deployment or use `kubectl scale deployment/ecom-web --replicas=6` to handle the increased load.
3. **Monitor Scaling**: Observe the deployment scaling up with `kubectl get pods`.
4. **Outcome**: The application scales up to handle increased traffic, showcasing Kubernetes' ability to manage application scalability dynamically.

### Step 8: Perform a Rolling Update

**Task**: Update the website to include a new promotional banner for the marketing campaign.

1. **Update Application**: Modify the web application's code to include the promotional banner.
2. **Build and Push New Image**: Build the updated Docker image as `yourdockerhubusername/ecom-web:v2` and push it to Docker Hub.
3. **Rolling Update**: Update `website-deployment.yaml` with the new image version and apply the changes.
4. **Monitor Update**: Use `kubectl rollout status deployment/ecom-web` to watch the rolling update process.
5. **Outcome**: The website updates with zero downtime, demonstrating rolling updates' effectiveness in maintaining service availability.

### Step 9: Roll Back a Deployment

**Task**: Suppose the new banner introduced a bug. Roll back to the previous version.

1. **Identify Issue**: After deployment, monitoring tools indicate a problem affecting user experience.
2. **Roll Back**: Execute `kubectl rollout undo deployment/ecom-web` to revert to the previous deployment state.
3. **Verify Rollback**: Ensure the website returns to its pre-update state without the promotional banner.
4. **Outcome**: The application's stability is quickly restored, highlighting the importance of rollbacks in deployment strategies.

### Step 10: Autoscale Your Application

**Task**: Automate scaling based on CPU usage to handle unpredictable traffic spikes.

1. **Implement HPA**: Create a Horizontal Pod Autoscaler targeting 50% CPU utilization, with a minimum of 2 and a maximum of 10 pods.
2. **Apply HPA**: Execute `kubectl autoscale deployment ecom-web --cpu-percent=50 --min=2 --max=10`.
3. **Simulate Load**: Use a tool like Apache Bench to generate traffic and increase CPU load.
4. **Monitor Autoscaling**: Observe the HPA in action with `kubectl get hpa`.
5. **Outcome**: The deployment automatically adjusts the number of pods based on CPU load, showcasing Kubernetes' capability to maintain performance under varying loads.

### Step 11: Implement Liveness and Readiness Probes

**Task**: Ensure the web application is restarted if it becomes unresponsive and doesn’t receive traffic until ready.

1. **Define Probes**: Add liveness and readiness probes to `website-deployment.yaml`, targeting an endpoint in your application that confirms its operational status.
2. **Apply Changes**: Update your deployment with the new configuration.
3. **Test Probes**: Simulate failure scenarios (e.g., manually stopping the application) and observe Kubernetes' response.
4. **Outcome**: Kubernetes automatically restarts unresponsive pods and delays traffic to newly started pods until they're ready, enhancing the application's reliability and availability.

### Step 12: Utilize ConfigMaps and Secrets

**Task**: Securely manage the database connection string and feature toggles without hardcoding them in the application.

1. **Create Secret and ConfigMap**: For sensitive data like DB credentials, use a Secret. For non-sensitive data like feature toggles, use a ConfigMap.
2. **Update Deployment**: Reference the Secret and ConfigMap in the deployment to inject these values into the application environment.
3. **Outcome**: Application configuration is externalized and securely managed, demonstrating best practices in configuration and secret management.

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
