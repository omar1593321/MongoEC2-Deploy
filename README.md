# MongoDB Deployment on EKS with Mongo Express 🚀

Welcome to my project, where I deployed MongoDB with Mongo Express on Amazon EKS (Elastic Kubernetes Service). This guide will walk you through the setup, deployment, and configuration of this stateful application on a managed Kubernetes service.

## 📂 Project Overview

In this project, I utilized Amazon EKS to deploy a MongoDB database and the Mongo Express web-based admin interface. The setup includes configuring persistent storage, network services, and addressing deployment challenges, all while leveraging the power of AWS’s managed Kubernetes service.

## 🔧 Key Features

- **Amazon EKS Setup:** Detailed instructions on setting up Amazon EKS, including creating a cluster and configuring `kubectl` to interact with it.
- **Persistent Storage:** Implemented PersistentVolumeClaims (PVC) and PersistentVolumes (PV) to ensure data persistence for MongoDB.
- **Service Exposure:** Configured Kubernetes services for MongoDB and Mongo Express to allow secure and reliable external access.
- **Troubleshooting and Optimization:** Documented challenges such as pod scheduling and node capacity constraints, with solutions applied to ensure smooth operation.
- **IAM Role and Policy Configuration:** Set up IAM roles and policies for managing EBS volumes and EKS access.
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
   ```
2. **Configure kubectl:**
Ensure kubectl is configured to interact with your new EKS cluster:  
```bash
aws eks --region <region> update-kubeconfig --name my-cluster
```
3. **Deploy MongoDB and Mongo Express:**
   Apply the Kubernetes YAML files for MongoDB and Mongo Express:
   ```bash
   kubectl apply -k github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/ecr # Install the EBS CSI Driver
   kubectl get csidrivers # Verify the CSI Driver is Registered You should see an entry for ebs.csi.aws.com.
   kubectl apply -f secret.yaml # to create the Secret called mongodb-secret
   kubectl apply -f mongodb-sc.yaml # to create the StorageClass called mongodb-sc.
   kubectl apply -f mongodb-pvc.yaml # to create the PersistentVolumeClaim called mongodb-pvc.
   # When deploying MongoDB on Kubernetes, the StorageClass automatically creates a new storage using Amazon Elastic Block Store (EBS) in AWS by provisioning a Persistent Volume (PV).
   kubectl apply -f mongodb.yaml #to create Deploument called mongodb-deployment and create the Service called mongodb-service.
   # Create a ConfigMap, which is used to store non-confidential information in key-value pairs. The ConfigMap will contain the mongo database url.
   kubectl apply -f mongodb-config.yaml # to create the Configmap called mongodb-configmap.
   # Create another Deployment . The Deployment will contain a Mongodb-Express Pod, which is a web-based interface to manage MongoDB databases. It will use the username and password from Secret, and the database url from       ConfigMap to access the MongoDB internal Service defined in mongodb.yaml.
   kubectl apply -f mongo-express.yaml # to create the Deployment called mongo-express and create the Service called mongo-express-service
   
   ```
 4. **Verify the Deployment:**
    Check the status of the pods, services, and persistent volumes:
    ```bash
    kubectl get pods
    kubectl get services
    kubectl get pv
    ```
  5. **Access Mongo Express:**
     
     Find the external IP or port of the Mongo Express service and navigate to it in your web browser to manage your MongoDB instance.
     
  6. **IAM Role and Policy Configuration:**

     Create an IAM Role for EBS CSI Driver:
        Go to the IAM console and create a new role.
        Select "EKS - Cluster" as the trusted entity.
        Attach the AmazonEBSCSIDriverPolicy policy to the role.

     Attach the IAM Role to Your EKS Nodes:
        Ensure your EKS worker nodes have the IAM role attached, allowing them to use the EBS CSI driver.
     
  7. **Port Configuration Details:**

     MongoDB Ports:
        MongoDB operates on the default port 27017. This port is exposed within the Kubernetes Service and the Deployment configuration, allowing communication between MongoDB and other services, like Mongo Express.
        Ensure that this port is properly configured in both the service and deployment YAML files to allow seamless database connectivity.

     Mongo Express Ports:
        Mongo Express, which provides a web-based admin interface for MongoDB, operates on port 8081.
        The Service for Mongo Express is configured as a LoadBalancer to expose this port to external traffic, allowing you to access the Mongo Express UI via your browser.
        Ensure your security groups, VPC settings, and service configuration correctly expose this port for external access.
     
**Configuration Files:**

- MongoDB Deployment YAML: Includes configurations for persistent storage and environment variables.

- Mongo Express Deployment YAML: Configures the web-based admin interface and service exposure.
       
🚀 **Usage**

- Manage MongoDB: Use Mongo Express to manage your MongoDB instance through a web interface.

- Monitor the Cluster: Utilize EKS monitoring tools and kubectl to keep an eye on cluster health and performance.
  
📜 Troubleshooting

- Pod Scheduling Issues: Address scheduling constraints by reviewing node capacity and resource requests.
- Data Persistence: Ensure PersistentVolumeClaims are properly bound to PersistentVolumes and check logs for any related errors.

  🎯 Conclusion

This project provides a comprehensive guide to deploying MongoDB and Mongo Express on Amazon EKS, offering practical experience with managed Kubernetes services, persistent storage, and cloud resource management.

Feel free to fork this repository and adapt the configurations to your own environment. Contributions and feedback are always welcome!

**Screen Shots**:

![Screenshot 2024-08-18 021032](https://github.com/user-attachments/assets/ace2d7c9-6c96-436f-b819-d714b02a018d)
![Screenshot 2024-08-18 021311](https://github.com/user-attachments/assets/75a9a9dc-95bc-47bf-8648-bf64bbaa3da9)

