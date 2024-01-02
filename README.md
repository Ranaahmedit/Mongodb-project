# Using k8s to deploy a MongoDB Database with a Mongo Express web-based Admin interface in aws 

![MongoDB-diagram](https://github.com/Ranaahmedit/Mongodb-project/assets/127610751/6bcc54a5-c86e-49d5-b5a7-3fa7cbe0d0fb)

## Architecture and features:
* The project will be deployed using a kubeadm cluster.
* The MongoDB Database will use Amazon EBS as the persistent storage to store data.

 ## General Concepts
 - A Pod is the smallest execution unit in Kubernetes, and an abstraction over containers. A container is a lightweight software that contains all the necessary tools, libraries and code to run an application.

  - `kubectl exec -it <pod_name> -- /bin/bash` to get a bash shell in the container.
  - `kubectl logs <pod_name>` to show information logged by a pod.

- A Deployment is a resource to describe how a ReplicaSet and Pod should behave.

  - `kubectl create deploy <deployment_name> --image=<image_name>` to create a basic deployment with minimal configurations.
  - `kubectl edit deploy <deployment_name>` to edit the configuration file of a deployment.
  - `kubectl delete deploy <deployment_name>` to delete a deployment.

- A ReplicaSet aims to maintain a stable set of Pods running at any given time. The number of Pods maintained is determined in the configuration file of a deployment.

- A Service exposes an application running on a set of Pods as a network service.

- A ConfigMap is used to store non-sensitive data in key-value pairs, and can be consumed as environment variables, command-line arguments, or as configuration files.

- A Secret is similar to a ConfigMap, but more towards storing sensitive data, such as passwords, OAuth tokens, and ssh keys.

  - `echo -n '<password>' | base64` to generate a base64 encoded string to be used as password in Secret, though a better hashing algorithm should be used.

## Getting Started

1 -  Create a Secret, which is used to store sensitive information. The Secret will contain the username and password for MongoDB.

- `kubectl apply -f mongodb-secret.yaml` to create the Secret called mongodb-pass.
- `kubectl delete -f mongodb-secret.yaml` to delete the Secret.

2 -  Create a  StorageClass 

- `kubectl apply -f mongodb-sc.yaml` to create the StorageClass called mongodb-sc.

3 -  Create a PersistentVolumeClaim 

- `kubectl apply -f mongodb-pvc.yaml` to create the PersistentVolumeClaim called mongodb-pvc.
   
4 -  Create a Deployment, When deploying MongoDB on Kubernetes, the StorageClass automatically creates a new storage using Amazon Elastic Block Store (EBS) in AWS by provisioning a Persistent            Volume (PV).

- `kubectl apply -f mongodb-deploy.yaml` to create Deploument called mongodb-deploy.
 
5 -  Create Service 

- `kubectl apply -f mongodb-svc.yaml` to create the Service called mongodb-svc.
  
6 -  Create a ConfigMap, which is used to store non-confidential information in key-value pairs. The ConfigMap will contain the mongo database url.

- `kubectl apply -f mongodb-cm.yaml` to create the Configmap called mongodb-cm.

7 - Create another Deployment . The Deployment will contain a Mongodb-Express Pod, which is a web-based interface to manage MongoDB databases. It will use the username and password from Secret,         and  the database url from ConfigMap to access the MongoDB internal Service defined in 4.

- `kubectl apply -f mongo-express-deploy.yaml ` to create the  Deployment called mongo-express-deploy

8 - create another service 
- `kubectl apply -f mongo-express-svc.yaml ` to create the Service called mongo-express-svc





  
  


 
