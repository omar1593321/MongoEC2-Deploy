# MongoDB Deployment on EKS with Mongo Express 🚀

Welcome to my project, where I deployed MongoDB with Mongo Express on Amazon EKS (Elastic Kubernetes Service). This guide will walk you through the setup, deployment, and configuration of this stateful application on a managed Kubernetes service.

## 📂 Project Overview

In this project, I utilized Amazon EKS to deploy a MongoDB database and the Mongo Express web-based admin interface. The setup includes configuring persistent storage, network services, and addressing deployment challenges, all while leveraging the power of AWS’s managed Kubernetes service.

## 🔧 Key Features

- **Amazon EKS Setup:** Detailed instructions on setting up Amazon EKS, including creating a cluster and configuring `kubectl` to interact with it.
- **Persistent Storage:** Implemented PersistentVolumeClaims (PVC) and PersistentVolumes (PV) to ensure data persistence for MongoDB.
- **Service Exposure:** Configured Kubernetes services for MongoDB and Mongo Express to allow secure and reliable external access.
- **Troubleshooting and Optimization:** Documented challenges such as pod scheduling and node capacity constraints, with solutions applied to ensure smooth operation.

## 🛠 Getting Started

### **Prerequisites:**

- An AWS account with permissions to create and manage EKS clusters, EC2 instances, and other resources.
- AWS CLI installed and configured.
- `eksctl` and `kubectl` installed.

### **Setup Instructions:**

1. **Create an EKS Cluster:**
   Use `eksctl` to create an EKS cluster:
   ```bash
   eksctl create cluster --name my-cluster --region <region> --nodes 2
