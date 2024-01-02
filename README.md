## Using k8s to deploy a MongoDB Database with a Mongo Express web-based Admin interface in aws 

# Architecture and features:
- The project will be deployed using a kubeadm cluster.
- The MongoDB Database will use Amazon EBS as the persistent storage to store data.


# Getting Started

1 - Create a Secret, which is used to store sensitive information. The Secret will contain the username and password for MongoDB.

'''
     kubectl apply -f mongodb-secret.yaml to create the Secret called mongodb-secret.
'''     
    - kubectl delete -f mongodb-secret.yaml to delete the Secret.
 
