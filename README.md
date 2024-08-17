MongoDB Deployment on EKS with Mongo Express 🚀

Welcome to my project, where I deployed MongoDB with Mongo Express on Amazon EKS (Elastic Kubernetes Service). This guide will walk you through the setup, deployment, and configuration of this stateful application on a managed Kubernetes service.

📂 Project Overview

In this project, I utilized Amazon EKS to deploy a MongoDB database and the Mongo Express web-based admin interface. The setup includes configuring persistent storage, network services, and addressing deployment challenges, all while leveraging the power of AWS’s managed Kubernetes service.

🔧 Key Features

    Amazon EKS Setup: Detailed instructions on setting up Amazon EKS, including creating a cluster and configuring kubectl to interact with it.
    
    Persistent Storage: Implemented PersistentVolumeClaims (PVC) and PersistentVolumes (PV) to ensure data persistence for MongoDB.
    
    Service Exposure: Configured Kubernetes services for MongoDB and Mongo Express to allow secure and reliable external access.
    
    Troubleshooting and Optimization: Documented challenges such as pod scheduling and node capacity constraints, with solutions applied to ensure smooth operation.
    

🛠 Getting Started

Prerequisites:

    An AWS account with permissions to create and manage EKS clusters, EC2 instances, and other resources.
    
    AWS CLI installed and configured.
    
    eksctl and kubectl installed.

Setup Instructions:

    Create an EKS Cluster:
    
    Use eksctl to create an EKS cluster:

   ```

eksctl create cluster --name my-cluster --region <region> --nodes 2

```
Configure kubectl:
Ensure kubectl is configured to interact with your new EKS cluster:

bash

aws eks --region <region> update-kubeconfig --name my-cluster

Deploy MongoDB and Mongo Express:
Apply the Kubernetes YAML files for MongoDB and Mongo Express:

bash

kubectl apply -f mongodb-deployment.yaml
kubectl apply -f mongo-express-deployment.yaml

Verify the Deployment:
Check the status of the pods, services, and persistent volumes:

bash

    kubectl get pods
    kubectl get services
    kubectl get pv

    Access Mongo Express:
    Find the external IP or port of the Mongo Express service and navigate to it in your web browser to manage your MongoDB instance.

Configuration Files:

    MongoDB Deployment YAML: Includes configurations for persistent storage and environment variables.
    Mongo Express Deployment YAML: Configures the web-based admin interface and service exposure.

🚀 Usage

    Manage MongoDB: Use Mongo Express to manage your MongoDB instance through a web interface.
    Monitor the Cluster: Utilize EKS monitoring tools and kubectl to keep an eye on cluster health and performance.

📜 Troubleshooting

    Pod Scheduling Issues: Address scheduling constraints by reviewing node capacity and resource requests.
    Data Persistence: Ensure PersistentVolumeClaims are properly bound to PersistentVolumes and check logs for any related errors.

🔗 Resources

    Amazon EKS Documentation
    Docker Installation Guide
    Kubernetes Documentation
    MongoDB Documentation

💬 Acknowledgements

Special thanks to my instructor for their invaluable guidance and support throughout this project. Your expertise helped navigate the complexities of EKS and Kubernetes deployments.
🎯 Conclusion

This project provides a comprehensive guide to deploying MongoDB and Mongo Express on Amazon EKS, offering practical experience with managed Kubernetes services, persistent storage, and cloud resource management.

Feel free to fork this repository and adapt the configurations to your own environment. Contributions and feedback are always welcome!
