# Trivy Installation and Usage Guide

## Installation and Commands in One Terminal Script

```sh
#!/bin/bash

# Install required dependencies
sudo apt-get install wget apt-transport-https gnupg lsb-release

# Add the Trivy GPG key
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

# Add the Trivy repository
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list

# Update the package list
sudo apt-get update

# Install Trivy
sudo apt-get install trivy

# Command to scan a Docker image
trivy image <image_name>

# Command to scan the filesystem for vulnerabilities and misconfigurations
trivy fs --security-checks vuln,config <folder_name_or_path>

# Command to scan a Docker image and filter results by severity (HIGH and CRITICAL)
trivy image --severity HIGH,CRITICAL <image_name>

# Command to scan a Docker image and save the results in JSON format
trivy image -f json -o results.json <image_name>

# Command to scan a Git repository for vulnerabilities
trivy repo <repo_url>

# Command to scan a Kubernetes cluster and generate a summary report
trivy k8s --report summary cluster
