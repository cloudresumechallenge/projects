| Challenge name | Cloud(s) | Challenge goal | Contributor |
| :--- | :--- | :--- | :--- |
| Working with data on Kubernetes | Google Cloud | Deploy a workload to Kubernetes to pull public data and import it into Elasticsearch or Prometheus for analysis. Completing this challenge means that you can work with Docker, Kubernetes, Helm, Prometheus or Elasticsearch, Grafana or Kibana, and a programming language. | [Daniel Dersch](https://sheepcode.substack.com/) |

## Challenge steps

### Install local Kubernetes
1. Install Kubernetes to your local machine. There are various options for accomplishing this; pick whichever one you want!
1. Install [these tools](https://kubernetes.io/docs/tasks/tools/) for working with Kubernetes.

### Choose a public time series data set
1. Browse [data.gov](https://data.gov) or a similar site for a time series data set that you are interested in.
1. The data set must be active and changing. In other words, there should be additional data in the future.

### Install either Elasticsearch and Kibana OR Prometheus and Grafana
1. Elasticsearch is an extremely popular search and analytics engine, and Kibana is the Web UI for working with data in Elasticsearch.
1. Prometheus is an extremely popular time series database, and Grafana is a Web UI for working with data in Prometheus.
1. You’ll be storing your public data in either Elasticsearch or Prometheus. The choice is up to you, so research both tools to determine which one is better for your data!
1. Use a tool like [Helm](https://helm.sh/) to install your chosen tool to your local Kubernetes.
1. Make sure you can login to Kibana (if you chose Elasticsearch) or Grafana (if you chose Prometheus) to complete this step.

### Write your importer program
1. Write a program that pulls your public time series data set from step 2 and imports it into Elasticsearch or Prometheus.
1. Use any programming language or shell you like for this step! Just make sure whatever you use has a good Elasticsearch or Prometheus library SDK.
1. Your program will likely need to transform the data into a structure compatible with either Elasticsearch or Prometheus.
1. The program must accept the URL of the public data set as a parameter.
1. You will likely have to parameterize this URL in your code with query strings.

### Write your Docker image
1. Write a Docker image that contains your program from step 4.
1. The Docker image must accept an environment variable named URL or URL_TEMPLATE that gets passed to your program.

### Run your Docker image as a container on Kubernetes
Run your docker image as a workload on Kubernetes. The workload should automatically run once per day every day to import new data.

### Visualize your data
1. Connect to Kibana Grafana and create a chart comparing time to some attribute of your data.
1. For instance, if your data was COVID-19 cases worldwide, you could create a chart with "Day" on the x-axis and "Count" on the y-axis.

### Create an actual Kubernetes cluster using a managed service in a public cloud
At the time of this writing, I recommend a Google Kubernetes Engine (GKE) cluster in a single zone, which should have minimal charges.

### Run your workload on your new cluster!
1. Install Elasticsearch/Kibana or Prometheus/Grafana to your cluster using Helm or a similar tool.
1. Run your Docker image as a container on the deployed Kubernetes.
1. Create your visualization on the cluster.

### Clean up and blog
Don’t forget to tear down your cloud resources when you are finished to avoid incurring ongoing expenses. Finally, write a blog post detailing your work!

### Extra credit - Deploy the other tool!
If you initially chose to deploy Prometheus, then deploy Elasticsearch this time - or vice versa. Then, either:
* Configure your Kubernetes cluster such that all metrics are sent to Prometheus, or
* Configure your Kubernetes cluster such that all logs are sent to Elasticsearch.

### Final takeaways
Kubernetes is the leading container-orchestration system, and Docker is the leading tool for building container images to run on Kubernetes. Elasticsearch and Kibana are key components of the ELK stack which thousands of organizations use for log analysis. Prometheus and Grafana are the most popular open-source tools for monitoring workloads on Kubernetes and other platforms. Every engineer on a DevOps team should be familiar with deploying and working with these tools.