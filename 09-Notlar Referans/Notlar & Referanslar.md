# 📚 Notlar & Referanslar

## ✅ Genel DevOps Hatırlatmaları

- DevOps = Geliştirme + Operasyon + Otomasyon
- Her şey versiyon kontrolüne girer (kod, pipeline, IaC)
- Güvenlik baştan düşünülmeli (shift-left security)
- Infrastructure as Code (IaC) → Terraform, Bicep
- CI = Build/Test, CD = Deploy/Release
- Monitoring & Alerting projenin kalbidir

---
## 🔄 Azure İçin En Yaygın CLI Komutları
```bash
# Login
az login

# Resource Group oluştur
az group create --name myRG --location westeurope

# VM başlat
az vm create --resource-group myRG --name myVM --image UbuntuLTS

# App Service oluştur
az webapp create --resource-group myRG --plan myPlan --name myApp --runtime "NODE|18-lts"

# Azure Kubernetes Cluster
az aks create --resource-group myRG --name myAKS --node-count 2 --generate-ssh-keys
```
---
## 🔗 Referans Kaynaklar

### 📘 Microsoft Learn (Resmi Kaynaklar)

- [Azure Fundamentals](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals/)
- [Azure DevOps Docs](https://learn.microsoft.com/en-us/azure/devops/)
- [Azure CLI Reference](https://learn.microsoft.com/en-us/cli/azure/)
- [Azure Monitor](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [Azure Kubernetes Service](https://learn.microsoft.com/en-us/azure/aks/)