## Docker command for deployment
1. Build docker image locally
```
docker build -t demotestmaven:latest .  
docker run -p 8082:8082 demotestmaven:latest 
```
2. Push docker image to docker hub 
```
docker login
docker tag demotestmaven:latest ngoc273/app:latest
docker push ngoc273/app:latest
```
3. Install and add ec2-user to docker group
sudo usermod -aG docker ec2-user
