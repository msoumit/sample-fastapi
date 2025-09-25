# Build Docker image (locally)
docker build -t sample-fastapi:local .

# Run Docker container (locally)
docker run -d -p 8000:8000 sample-fastapi:local

# Tag image for ACR
docker tag sample-fastapi:local acrmsoumiteastus01.azurecr.io/sample-fastapi:v1

# Push image to ACR
docker push acrmsoumiteastus01.azurecr.io/sample-fastapi:v1

# Run Docker container from ACR image (Optional)
docker run -d -p 8000:8000 acrmsoumiteastus01.azurecr.io/sample-fastapi:v1

# Connect AKS with kubectl
az aks get-credentials --resource-group rg-msoumit-eastus-01 --name aks-cluster-msoumit-eastus-01

# Verify cluster connection
kubectl get nodes

# Deploy app to AKS
kubectl apply -f k8s.yml

# Check pods
kubectl get pods
kubectl describe pod -l app=sample-fastapi
# Get service endpoint details
kubectl get svc

# Optional Debugging
kubectl logs <pod-name>
kubectl describe svc sample-fastapi