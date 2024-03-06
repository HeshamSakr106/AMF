# Access and Mobility Management Function (AMF)
# Jenkins Pipeline for 5G AMF Deployment
This Jenkins pipeline script automates the deployment process of the 5G Access and Mobility Management Function (AMF) using Docker containers and Helm charts.

# Pipeline Overview
The pipeline consists of the following stages:

Verify Branch: Echoes the current Git branch being built.

Login to Dockerhub: Logs in to Dockerhub using credentials stored in Jenkins.

Pulling base image from Dockerhub: Pulls the base Docker image for the AMF from Dockerhub.

docker build: Builds a new Docker image for the 5G AMF application.

Scan Image for Common Vulnerabilities and Exposures: Uses Trivy to scan the Docker image for common vulnerabilities and exposures (CVEs).

Pushing to Dockerhub: Pushes the newly built Docker image to Dockerhub.

Build and Package Helm Chart: Packages the Helm chart for deployment.

Configure Kubernetes Context: Configures the Kubernetes context for deployment.

Deploy Helm Chart on EKS: Deploys the Helm chart on Amazon Elastic Kubernetes Service (EKS).

# Prerequisites
Jenkins with necessary plugins installed (GitHub plugin, Docker plugin, Credentials plugin).
AWS CLI installed with appropriate permissions to interact with EKS.
Docker installed on Jenkins agent nodes.
Trivy installed on Jenkins agent nodes for vulnerability scanning.
# Usage
Ensure that Jenkins is properly configured with necessary plugins and credentials.
Create a new Jenkins pipeline job and configure it to use this pipeline script.
Trigger the pipeline manually or set up automatic triggers as per your requirements.
# Notes
This pipeline assumes that Docker images are hosted on Dockerhub.
Replace placeholders (e.g., credentials IDs, Docker image names) with actual values relevant to your setup.
# References
Trivy
Dockerhub
Helm
