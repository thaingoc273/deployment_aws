1. Initialise terraform

``
terraform init
terraform plan
terraform apply
terraform destroy
``

2. Deploy ecr in the cloud

```
cd terraform

# 1. Init and apply
terraform init
terraform apply -auto-approve

# 2. Get ECR URL
export ECR_URL=$(terraform output -raw ecr_repo_url)

#   $env:ECR_URL = $(terraform output -raw ecr_repo_url) for windows

# 3. Login to ECR
aws ecr get-login-password --region us-east-1 | \
    docker login --username AWS --password-stdin $ECR_URL


docker login -u AWS -p "$(aws ecr get-login-password --region eu-central-1)" 480609331633.dkr.ecr.eu-central-1.amazonaws.com # this one works

# 4. Build and push Docker image
cd ../docker
docker build -t myapp .
docker tag myapp:latest $ECR_URL:latest
docker push $ECR_URL:latest

# 5. Force new ECS deployment to pick up new image
cd ../terraform
terraform apply -auto-approve
```
