# 🛠️ Azure DevOps Pipelines – CI/CD Süreçleri

## 🧠 Amaç

Azure Pipelines ile sürekli entegrasyon (CI) ve sürekli teslimat/dağıtım (CD) süreçlerinin nasıl kurulduğunu öğrenmek.

---
## 🔍 Azure Pipelines Nedir?

Azure Pipelines, yazılımın otomatik olarak test edilmesini, derlenmesini ve hedef ortamlara dağıtılmasını sağlayan CI/CD hizmetidir.

- **CI (Continuous Integration)**: Kod birleştirme sonrası otomatik test/derleme süreci
- **CD (Continuous Delivery/Deployment)**: Testten geçen kodun staging/prod ortamına otomatik taşınması

---
## 🧱 Pipeline Türleri

| Tür          | Açıklama |
|--------------|----------|
| **YAML Pipeline** | Kodla tanımlanan pipeline (as code) – `.yml` dosyası ile |
| **Classic Pipeline** | UI üzerinden tıklayarak oluşturulan geleneksel pipeline |
*Not: YAML pipeline tercih edilmesi önerilir. Kaynak kod ile birlikte versiyonlanır.*

---
## 📄 Basit YAML Pipeline Örneği

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

steps:
  - task: NodeTool@0
    inputs:
      versionSpec: '16.x'
    displayName: 'Install Node.js'

  - script: npm install
    displayName: 'Install Dependencies'

  - script: npm run build
    displayName: 'Build Project'

  - script: npm test
    displayName: 'Run Tests'
```
## 🔧 Pipeline Adımları (Steps)

- **Tasks**: Ön tanımlı görevler (örneğin: `CopyFiles`, `PublishBuildArtifacts`)
- **Scripts**: Shell/PowerShell komutları çalıştırmak
- **Variables**: Ortak değişkenler tanımlama
- **Stages / Jobs**: Pipeline aşamalarını gruplamak
## 💼 Pipeline Ortamları

| Ortam                      | Açıklama                                   |
| -------------------------- | ------------------------------------------ |
| **Self-hosted agent**      | Kendi sunucunda çalışan agent              |
| **Microsoft-hosted agent** | Azure’un sağladığı geçici build makineleri |

---
## 🔁 Trigger Türleri

- `trigger:` → Branch tetikleme (örn: push sonrası çalıştır)
- `pr:` → Pull request tetikleme
- `schedule:` → Zamanlanmış çalıştırma

---
## 🔐 Güvenlik

- Secrets → Azure Key Vault ile entegre
- `env:` → Ortam değişkeni olarak geçici kullanma
- RBAC → Pipeline yazma/çalıştırma yetkileri

---
## 💡 İpuçları

- Her pipeline bir `.yml` dosyasıdır, genelde `.azure-pipelines.yml` olarak adlandırılır.
- Her adımda `displayName` kullanmak çıktıyı kolaylaştırır.
- Pipeline başarısız olursa son çıktıları incele (`Logs` sekmesinden).

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops](https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/yaml-schema](https://learn.microsoft.com/en-us/azure/devops/pipelines/yaml-schema)