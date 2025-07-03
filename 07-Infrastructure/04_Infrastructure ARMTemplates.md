# 📐 Azure DevOps – ARM Templates ile Altyapı Tanımlama

## 🧠 Amaç

Azure altyapısını **JSON formatındaki ARM Templates** ile tanımlamak ve Azure DevOps pipeline’ı üzerinden bu tanımları uygulamayı öğrenmek.

---
## 🔍 ARM Template Nedir?

- Azure üzerinde kaynak oluşturmak için kullanılan **JSON tabanlı** tanım dosyalarıdır.
- Azure Resource Manager (ARM) tarafından yorumlanarak altyapı kaynakları oluşturulur.
- Deterministik, sürülebilir ve tekrar edilebilir altyapı oluşturur.

---
## 🔧 Yapı

### 1. `template.json` – Kaynak tanımları
### 2. `parameters.json` – Giriş parametreleri

---
## 📦 Örnek ARM Template

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountName": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2022-09-01",
      "name": "[parameters('storageAccountName')]",
      "location": "westeurope",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {}
    }
  ]
}
```
---
## 🧪 Azure DevOps ile ARM Template Deploy

### 1. Azure Service Connection oluştur

### 2. `template.json` ve `parameters.json` dosyalarını repo’ya ekle

### 3. YAML Pipeline:
```yaml
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: AzureResourceManagerTemplateDeployment@3
  inputs:
    deploymentScope: 'Resource Group'
    azureResourceManagerConnection: 'my-service-connection'
    subscriptionId: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
    action: 'Create Or Update Resource Group'
    resourceGroupName: 'rg-dev'
    location: 'westeurope'
    templateLocation: 'Linked artifact'
    csmFile: 'templates/template.json'
    csmParametersFile: 'templates/parameters.json'
```
---
## 🔐 Güvenlik

|Konu|Öneri|
|---|---|
|Parametre dosyası|Gizli bilgileri `.parameters.json` içinde tutma|
|Erişim kontrolü|RBAC ile Azure bağlantılarını sınırla|
|Template doğrulama|`az deployment validate` komutunu kullan|

---
## 💡 İpuçları

- Uzun ve karmaşık yapıların yönetimi zor olabilir → Bicep önerilir.
- `defaultValue`, `allowedValues` gibi özelliklerle kullanıcı girişlerini sınırla.
- Deployment modunu dikkatli seç (`Incremental` vs `Complete`).

---
## ARM vs Bicep vs Terraform

|Özellik|ARM Template|Bicep|Terraform|
|---|---|---|---|
|Format|JSON|Bicep DSL|HCL|
|Azure’a özel|✅|✅|❌ (çoklu bulut)|
|Okunabilirlik|Düşük|Yüksek|Orta|
|Kod tekrar kullanımı|Zor|Kolay|Kolay|
|Entegrasyon|Yüksek|Yüksek|Orta|

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/overview
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment)