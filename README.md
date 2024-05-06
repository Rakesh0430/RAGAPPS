deployment steps in azure from azure cli:
az --version
az login
az group create --name my-fastapi-india-rg --location centralindia
az acr create --name mynewacrforindia --resource-group my-fastapi-india-rg --sku Basic
docker build -t mynewacrforindia.azurecr.io/my-fastapi-app:latest .
az acr login --name mynewacrforindia 
docker push mynewacrforindia.azurecr.io/my-fastapi-app:latest 
az appservice plan create --name my-fastapi-plan --resource-group my-fastapi-india-rg --is-linux --sku B1 
az webapp create --resource-group my-fastapi-india-rg --plan my-fastapi-plan --name my-fastapi-app --deployment-container-image-name mynewacrforindia.azurecr.io/my-fastapi-app:latest
az webapp delete --name my-fastapi-app --resource-group my-fastapi-india-rg #delete the resource group and its dependencies
