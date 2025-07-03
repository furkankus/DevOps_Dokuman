# 🧱 Azure DevOps – Bicep ile Altyapı Tanımlama

## 🧠 Amaç

Azure üzerinde kaynakları tanımlamak için Bicep dilini kullanarak daha sade, modüler ve okunabilir Infrastructure as Code çözümleri üretmeyi öğrenmek.

---
## 🔍 Bicep Nedir?

- Azure’un yeni nesil **Infrastructure as Code (IaC)** dilidir.
- JSON tabanlı **ARM template’lerin** daha okunabilir versiyonudur.
- Azure CLI, PowerShell veya DevOps pipeline’ları ile kolayca entegre olur.

---
## 📦 Basit Bicep Örneği (Resource Group)
```bicep
resource rg 'Microsoft.Resources/resourceGroups@2021-04-01' = {
  name: 'rg-bicep-demo'
  location: 'westeurope'
}
```
*Bu kod, belirtilen konumda bir kaynak grubu oluşturur.*

---
## 🔧 Bicep Kurulumu (Lokal Kullanım)
```bash
az bicep install
```
*Azure CLI içinden doğrudan yüklenebilir. Ekstra paket yöneticisine gerek yoktur.*

---
## 📦 Azure Pipeline ile Bicep Kullanımı

### 1. Bicep dosyanı repo'ya ekle (örneğin `main.bicep`)

### 2. Azure Service Connection oluştur

### 3. YAML Pipeline Örneği:
```yaml
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: AzureCLI@2
  inputs:
    azureSubscription: 'my-service-connection'
    scriptType: 'bash'
    scriptLocation: 'inlineScript'
    inlineScript: |
      az deployment sub create \
        --location westeurope \
        --template-file infrastructure/main.bicep
```
---
## 🛠️ Parametreli Kullanım
```bicep
param rgName string = 'rg-bicep-demo'

resource rg 'Microsoft.Resources/resourceGroups@2021-04-01' = {
  name: rgName
  location: 'westeurope'
}
```
CLI ile:
```bash
az deployment sub create \
  --location westeurope \
  --template-file main.bicep \
  --parameters rgName='rg-dev'
```
---
## 🧰 Bicep vs ARM Template

|Özellik|ARM Template (JSON)|Bicep|
|---|---|---|
|Okunabilirlik|Düşük|Yüksek|
|Kod tekrar kullanımı|Karmaşık|Kolay|
|Dosya boyutu|Büyük|Küçük|
|Native destek|Var|Artan şekilde destekleniyor|

---
## 🔐 Güvenlik Pratikleri

- Parametre dosyalarında **secret** bilgi saklamaktan kaçın
- Pipeline üzerinden **secure variable** ile aktar
- Bicep ile Azure Key Vault kaynaklarını da oluşturabilir ve entegre edebilirsin

---

## 💡 İpuçları

- `bicep build` ile `.json` çıktısı alabilirsin
- `bicep lsp` desteği ile Visual Studio Code’da autocomplete + syntax kontrol alırsın
- Modül sistemi ile büyük yapıları bölerek yönetebilirsin

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview)
- [https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/tutorial-deploy-infrastructure](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/tutorial-deploy-infrastructure)