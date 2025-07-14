## 1. Create ecr repository
```
aws ecr create-repository --repository-name my-app-repo

```
## 2. Login to ECR
```
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.eu-central-1.amazonaws.com
```
## 3. Build docker image
```
docker build -t my-app .
```
## 4. Tag docker image

```
docker tag my-app:latest 123456789012.dkr.ecr.eu-central-1.amazonaws.com/my-app:latest
```
## 5. Push docker image to ECR
```
docker push 123456789012.dkr.ecr.eu-central-1.amazonaws.com/my-app:latest
```

``
aws ecr describe-repositories
aws ecr delete-repository --repository-name apptest --force 
``