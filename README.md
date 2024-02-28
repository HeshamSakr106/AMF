# 5G-amf
# Checkout Repository: 
This step checks out your GitHub repository so that subsequent steps can access your repository's files.

# Login to Docker Hub: 
It logs in to Docker Hub using the provided credentials stored as GitHub secrets.

# Pull Base Image from Docker Hub: 

This step pulls the base Docker image (abodiaa/amf-base:latest) from Docker Hub.

# Docker Build: 
It builds a new Docker image (abodiaa/5g-amf:latest) from the Dockerfile in the repository.

# Scan Image for CVEs: 
This step scans the newly built Docker image for Common Vulnerabilities and Exposures (CVEs) using Trivy and outputs the scan report to trivy-report.json.

# Push to Docker Hub: 
It pushes the newly built Docker image to Docker Hub.

# Build and Package Helm Chart: 
This step packages the Helm chart located in the helm/ directory.

# Configure Kubernetes Context: 
It configures the Kubernetes context for the AWS EKS cluster named 5G-Core-Net.

#
Deploy Helm Chart on EKS: 
<<<<<<< HEAD
This step deploys the Helm chart (amf) on the configured EKS cluster.
=======
This step deploys the Helm chart (amf) on the configured EKS cluster.
>>>>>>> 5c174eede6ddcaaeb8e1da08f57ebf5a55d1f91d
