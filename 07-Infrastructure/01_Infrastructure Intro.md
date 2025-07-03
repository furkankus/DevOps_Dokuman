# 🏗️ Azure DevOps – Infrastructure as Code (IaC) Giriş

## 🧠 Amaç

Azure DevOps ortamında altyapı kaynaklarını kodla tanımlayarak versiyon kontrolü, tekrar kullanılabilirlik ve otomasyon sağlamayı öğrenmek.

---
## 🌐 Infrastructure as Code Nedir?

- **Altyapının (sunucu, ağ, disk, veri tabanı vb.) kodla tanımlanmasıdır.**
- Azure DevOps pipeline’larıyla entegre edilerek her şeyin otomatik ve sürülebilir hale gelmesi sağlanır.
- Terraform, Bicep, ARM Template, Ansible gibi araçlar kullanılır.

---
## 🚀 Avantajları

| Özellik                 | Açıklama |
|-------------------------|----------|
| **Versiyon Kontrolü**      | Altyapı kodları Git ile versiyonlanabilir |
| **Tekrarlanabilirlik**     | Aynı ortamı tekrar tekrar oluşturma imkânı |
| **Otomasyon**              | CI/CD süreçlerine dahil edilebilir |
| **Hata Azaltımı**          | Elle müdahale yerine tanımlı yapı ile daha az hata |
| **Denetlenebilirlik**      | Değişikliklerin kim tarafından, ne zaman yapıldığı izlenebilir |

---
## 🛠️ Kullanılan IaC Araçları

| Araç      | Açıklama |
|-----------|----------|
| **Terraform** | En yaygın ve bulut bağımsız altyapı otomasyon aracı |
| **Bicep**     | Azure'a özel modern ve okunabilir bir IaC dili |
| **ARM Template** | Azure’un JSON tabanlı geleneksel altyapı tanımı |
| **Ansible**  | Daha çok yapılandırma ve provision işlemleri için kullanılır |
| **Pulumi**   | Kod tabanlı IaC (Python, TypeScript vb. destekler) |

---
## 🔁 Azure DevOps ile Entegrasyon

1. Infrastructure kodlarını Git reposunda tut
2. Pipeline ile bu kodları çalıştır:
   - `Terraform init/plan/apply`
   - `az deployment group create`
3. Otomatik ortam oluştur (örneğin dev, test, prod)

---
## 📦 Azure Örneği: Bicep

```bicep
resource storageAccount 'Microsoft.Storage/storageAccounts@2022-09-01' = {
  name: 'myuniquestorageacct'
  location: 'eastus'
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
}
```
---
### 🤖 Pipeline Örneği (Terraform)
```yaml
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: TerraformInstaller@1
  inputs:
    terraformVersion: '1.5.0'

- script: terraform init
- script: terraform plan
- script: terraform apply -auto-approve
```
---
## 🔐 Güvenlik ve Best Practice

- Service Connection ile Azure’a erişimi kontrollü sağla
- State dosyalarını Azure Storage üzerinde sakla (Terraform için)
- Sensitive değerleri pipeline variable ya da Key Vault üzerinden yönet

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/infrastructure-as-code/](https://learn.microsoft.com/en-us/azure/devops/pipelines/infrastructure-as-code/)
- [https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/)
- https://developer.hashicorp.com/terraform