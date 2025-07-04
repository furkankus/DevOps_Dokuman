# 🔗 Azure Cloud – Azure DevOps Entegrasyonu

## 🧠 Amaç

Azure kaynaklarının Azure DevOps ile nasıl entegre edildiğini öğrenmek ve CI/CD süreçlerini otomatikleştirmek.

---
## ⚙️ 1. Azure DevOps Nedir?

- Microsoft’un sunduğu CI/CD, kod versiyonlama, artefact, test yönetimi ve izleme platformudur.
- Azure hizmetleriyle doğrudan entegre çalışır.

---
## 🔑 2. Azure Service Connection (Hizmet Bağlantısı)

Azure kaynaklarına Azure DevOps içerisinden erişmek için kullanılır.  
Genellikle bir **Service Principal** üzerinden yetkilendirilir.

### ✍️ Azure CLI ile SPN Oluşturma

```bash
az ad sp create-for-rbac \
  --name "devops-connection" \
  --role contributor \
  --scopes /subscriptions/<subscription-id>
```
---
### 📌 Azure DevOps’ta Tanımlama

- Project Settings → Service Connections → Azure Resource Manager
- SP bilgilerini gir ve bağla

---
## 📦 3. Uygulama Dağıtımı

Azure DevOps pipeline ile aşağıdaki servislere otomatik deploy yapılabilir:

|Servis|Açıklama|
|---|---|
|**App Service**|Web uygulamaları|
|**Azure Function**|Sunucusuz uygulamalar|
|**Azure VM**|Script/agent ile|
|**AKS**|YAML/Helm ile dağıtım|
|**Blob Storage**|Statik web dosyaları|

---
### 📄 4. Örnek Azure App Service Deploy (YAML)
```yaml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: ubuntu-latest

variables:
  azureSubscription: 'MyAzureServiceConnection'
  appName: 'myappservice'
  resourceGroup: 'myRG'

stages:
- stage: Deploy
  jobs:
  - job: DeployApp
    steps:
    - task: AzureWebApp@1
      inputs:
        azureSubscription: $(azureSubscription)
        appType: webApp
        appName: $(appName)
        package: '$(System.DefaultWorkingDirectory)/**/*.zip'
```
---
## 📦 5. Terraform veya Bicep ile Altyapı Yönetimi

Pipeline ile Azure kaynakları Infrastructure as Code (IaC) olarak yönetilebilir.

- Terraform örneği:
```yaml
- task: TerraformCLI@0
  inputs:
    command: 'apply'
    environmentServiceName: 'MyAzureServiceConnection'
```
---
## 🔐 6. Güvenli Dağıtım

|Özellik|Açıklama|
|---|---|
|**Stages**|Dev → Test → Prod ortamları|
|**Approvals**|Manual onay mekanizması|
|**Secrets**|Azure Key Vault ile şifre yönetimi|
|**RBAC**|Servis bağlantılarına kısıtlı yetki|

---
## 🔁 7. İzleme ve Geri Bildirim

- Azure Monitor ve Application Insights ile performans ve hata izleme
- Deployment logs ve build output kayıtları

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/](https://learn.microsoft.com/en-us/azure/devops/)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/](https://learn.microsoft.com/en-us/azure/devops/pipelines/)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints)