# 🌍 Azure DevOps – Terraform ile Altyapı Otomasyonu

## 🧠 Amaç

Azure DevOps üzerinde Terraform kullanarak bulut altyapı kaynaklarının tanımlanması, sürdürülmesi ve otomatik olarak yönetilmesini öğrenmek.

---
## 🌐 Terraform Nedir?

- **Açık kaynaklı** ve **bulut bağımsız** bir altyapı tanım aracıdır.
- YAML değil, kendi HCL (HashiCorp Configuration Language) dilini kullanır.
- Azure, AWS, GCP, Kubernetes gibi birçok sağlayıcıyı destekler.

---
## 🏗️ Temel Terraform Yapısı

1. **main.tf** – kaynak tanımları
2. **variables.tf** – parametre tanımları
3. **outputs.tf** – çıktıların tanımlanması
4. **terraform.tfstate** – mevcut altyapı durumu

---
## 📦 Basit Azure Resource Group Örneği

```hcl
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "dev_rg" {
  name     = "rg-dev"
  location = "East US"
}
```
---

## 🧪 Azure DevOps Pipeline ile Terraform Kullanımı
### 1. Azure Service Connection oluştur (RBAC ile)
### 2. YAML Pipeline Örneği:
```yaml
trigger:
- main

pool:
  vmImage: ubuntu-latest

variables:
  backend_rg: 'rg-terraform'
  backend_sa: 'tfstateaccount'
  backend_container: 'tfstate'

steps:
- task: TerraformInstaller@1
  inputs:
    terraformVersion: '1.5.0'

- script: terraform init
  workingDirectory: 'infra/'

- script: terraform plan
  workingDirectory: 'infra/'

- script: terraform apply -auto-approve
  workingDirectory: 'infra/'
```
---
### 🧱 Terraform Backend Kullanımı (State Yönetimi)
```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-terraform"
    storage_account_name = "tfstateaccount"
    container_name       = "tfstate"
    key                  = "dev.terraform.tfstate"
  }
}
```
*State dosyaları Azure Storage Account’ta tutulur. Ekip içi senkronizasyon için kritiktir.*

---
## 🔐 Güvenlik

|Konu|Önlem|
|---|---|
|Secret erişimi|Azure Key Vault ile entegre et|
|SP yetkilendirme|Minimum yetki ilkesi (Reader, Contributor, vs.)|
|Locking|Aynı anda apply çalışmasını engelle|

---
## 💡 İpuçları

- Terraform modülleri ile tekrar kullanılabilirlik sağla.
- `terraform validate` ile kod kalitesini test et.
- `terraform destroy` ile ortamı tamamen kaldırabilirsin.
- Dev/Test/Prod için farklı `tfvars` dosyaları kullan.

---
## 🔗 Kaynaklar

- https://developer.hashicorp.com/terraform
- [https://learn.microsoft.com/en-us/azure/developer/terraform/overview](https://learn.microsoft.com/en-us/azure/developer/terraform/overview)
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs