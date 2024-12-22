# Helm Installation Guide for Ubuntu

This guide will walk you through the process of installing **Helm** on an **Ubuntu** system. Helm is a powerful package manager for Kubernetes that helps you define, install, and manage Kubernetes applications.

## Prerequisites

- Ubuntu 18.04 or later
- A working internet connection
- `sudo` privileges on your machine

---

## Table of Contents

- [Step 1: Update the System](#step-1-update-the-system)
- [Step 2: Install Dependencies](#step-2-install-dependencies)
- [Step 3: Add Helm Repository](#step-3-add-helm-repository)
- [Step 4: Install Helm](#step-4-install-helm)
- [Step 5: Verify the Installation](#step-5-verify-the-installation)
- [Step 6: Optional - Troubleshooting Duplicate Repository Warnings](#step-6-optional---troubleshooting-duplicate-repository-warnings)
- [Step 7: Optional - Using Helm](#step-7-optional---using-helm)

---

## Step 1: Update the System

Before installing any packages, it's a good practice to update your system:

```bash
sudo apt-get update
```
## Step 2: Install Dependencies
#### Helm requires some dependencies to be installed, such as curl and apt-transport-https. You can install them by running the following command:

```bash
sudo apt-get install -y curl apt-transport-https
```
## Step 3: Add Helm Repository
#### You need to add the official Helm repository to your system. Run the following commands:

Download and install the Helm GPG key:

```bash
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
```
Add the Helm APT repository:

```bash
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://baltocdn.com/helm/stable/debian/ all main"
```
## Step 4: Install Helm
#### Once the repository is added, update your package list:

```bash
sudo apt-get update
```
Now you can install Helm:

```bash
sudo apt-get install helm
```
## Step 5: Verify the Installation
#### After installation, you can verify that Helm was successfully installed by checking its version:

```bash
helm version
```
You should see output like this (with the version number matching the latest release):

```
version.BuildInfo{Version:"v3.16.4", GitCommit:"7877b45b63f95635153b29a42c0c2f4273ec45ca", GitTreeState:"clean", GoVersion:"go1.22.7"}
```
## Step 6: Optional - Troubleshooting Duplicate Repository Warnings
#### If you see warnings about duplicate entries (e.g., google-cloud-sdk.list), it means that some repository entries are duplicated in your system configuration. To resolve this:

Inspect the file:

Open the google-cloud-sdk.list file:

```bash
sudo nano /etc/apt/sources.list.d/google-cloud-sdk.list
```
Remove duplicate lines:

##### Identify and remove any duplicated lines that reference the same repository.

Save and exit:

After removing the duplicates, save and close the file (Ctrl + X, then Y to confirm).

Update the package list:

Run the following command to refresh your repositories:

```bash
sudo apt-get update
```
## Step 7: Optional - Using Helm
#### Add a Helm Chart Repository
For example, to add the stable chart repository:

```bash
helm repo add stable https://charts.helm.sh/stable
helm repo update
```
#### Install a Helm Chart
You can install a Helm chart, such as the NGINX Ingress Controller:

```bash
helm install my-nginx-ingress stable/nginx-ingress
```
List Installed Helm Releases
To view the Helm releases in your cluster:

```bash
helm list
```
#### Upgrade a Helm Release
If you need to upgrade a Helm release:

```bash
helm upgrade my-nginx-ingress stable/nginx-ingress
```
#### Uninstall a Helm Release
To uninstall a Helm release:

```bash
helm uninstall my-nginx-ingress
```
## Conclusion
- You have successfully installed Helm on your Ubuntu system! Helm is now ready to manage your Kubernetes applications. If you encounter any issues or need help, feel free to consult the official Helm documentation at https://helm.sh/docs/.