## EKS deployment
🚀 Big picture

Docker image (in ECR) → Kubernetes Deployment in EKS → Exposed via Service / LoadBalancer


- ECR stores your built Docker image.

- EKS runs your containers using Kubernetes.

- You use kubectl + deployment.yaml + service.yaml to tell EKS what to run.

🛠 Step 1: Ensure EKS cluster & kubectl set up
If you don’t have your cluster & config yet, run:

bash
Copy
Edit
eksctl create cluster --name my-cluster --region us-west-2
Or use AWS Console → EKS → Create cluster.

Then configure kubectl:

```
aws eks --region us-west-2 update-kubeconfig --name my-cluster
```

✅ Test:
```
kubectl get nodes
```
You should see worker nodes ready.

🛠 Step 2: Make sure EKS nodes can pull from ECR
AWS EKS-managed nodes usually come with IAM policies that allow pulling from ECR.
By default, if you’re using eksctl, it attaches the policy AmazonEC2ContainerRegistryReadOnly.

Verify IAM role attached to your worker nodes includes AmazonEC2ContainerRegistryReadOnly.

🛠 Step 3: Write Kubernetes manifests
✅ a. deployment.yaml
Create a deployment.yaml telling Kubernetes to pull from ECR and run it.

🛠 Step 4: Deploy to EKS
Run:
```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
🛠 Step 5: Get your LoadBalancer URL
```
kubectl get svc
```

🚀 Summary cheat sheet

✅ Deploy your ECR image to EKS

```
# (make sure kubectl is pointing to EKS cluster)
aws eks --region us-west-2 update-kubeconfig --name my-cluster

# apply manifests
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# check everything
kubectl get deployments
kubectl get pods
kubectl get svc
```

### Delete eks cluster

```
eksctl delete cluster --name YOUR_CLUSTER_NAME

```