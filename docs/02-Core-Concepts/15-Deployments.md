# Deployments
  - Take me to [Video Tutorial](https://kodekloud.com/topic/deployments-3/)

In this section, we will take a look at kubernetes deployments

#### Deployment is a kubernetes object. 
  
 ![deployment](../../images/deployment.PNG)
  
#### How do we create deployment?

```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: myapp-deployment
      labels:
        app: myapp
        type: front-end
    spec:
     template:
        metadata:
          name: myapp-pod
          labels:
            app: myapp
            type: front-end
        spec:
         containers:
         - name: nginx-container
           image: nginx
     replicas: 3
     selector:
       matchLabels:
        type: front-end
 ```
- Once the file is ready, create the deployment using deployment definition file
  ```
  $ kubectl create -f deployment-definition.yaml
  ```
- To see the created deployment
  ```
  $ kubectl get deployment
  ```
- The deployment automatically creates a **`ReplicaSet`**. To see the replicasets
  ```
  $ kubectl get replicaset
  ```
- The replicasets ultimately creates **`PODs`**. To see the PODs
  ```
  $ kubectl get pods
  ```
    
  ![deployment1](../../images/deployment1.PNG)
  
- To see the all objects at once
  ```
  $ kubectl get all
  ```
  ![deployment2](../../images/deployment2.PNG)
  
  Certification Tip!
Here’s a tip!

As you might have seen already, it is a bit difficult to create and edit YAML files. Especially in the CLI. During the exam, you might find it difficult to copy and paste YAML files from browser to terminal. Using the kubectl run command can help in generating a YAML template. And sometimes, you can even get away with just the kubectl run command without having to create a YAML file at all. For example, if you were asked to create a pod or deployment with specific name and image you can simply run the kubectl run command.

Use the below set of commands and try the previous practice tests again, but this time try to use the below commands instead of YAML files. Try to use these as much as you can going forward in all exercises

Reference (Bookmark this page for exam. It will be very handy):

https://kubernetes.io/docs/reference/kubectl/conventions/

Create an NGINX Pod

kubectl run nginx --image=nginx

Generate POD Manifest YAML file (-o yaml). Don’t create it(–dry-run)

kubectl run nginx --image=nginx --dry-run=client -o yaml

Create a deployment

kubectl create deployment --image=nginx nginx

Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run)

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run) with 4 Replicas (–replicas=4)

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.

kubectl create -f nginx-deployment.yaml

OR

In k8s version 1.19+, we can specify the –replicas option to create a deployment with 4 replicas.

kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
  
K8s Reference Docs:
- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/
- https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/
- https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/
