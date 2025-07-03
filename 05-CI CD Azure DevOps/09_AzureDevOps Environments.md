# 🌐 Azure DevOps Environments – Ortam Tanımlamaları ve Yönetimi

## 🧠 Amaç

Azure DevOps Environments kullanarak uygulamanın dağıtıldığı fiziksel veya mantıksal ortamları yönetmeyi, izlemeyi ve kontrol etmeyi öğrenmek.

---
## 🔍 Environment (Ortam) Nedir?

- Bir uygulamanın dağıtıldığı yer (örn: `Development`, `Test`, `Staging`, `Production`)
- Ortam bazlı onay, denetim ve izin politikaları tanımlanabilir.
- Deployment geçmişi, logları ve kullanıcı onayları tek yerden takip edilir.

---
## 🧱 Ortam Türleri

| Ortam Türü       | Açıklama                           |
|------------------|------------------------------------|
| **Virtual Machine** | Fiziksel ya da sanal makineler |
| **Kubernetes**   | AKS veya kendi K8s cluster'ınız    |
| **Azure App Service** | Azure’un PaaS hizmeti         |
| **Generic (resource yok)** | Scriptlerle çalışan basit ortam |

---
## 🛠️ Environment Oluşturma

1. Azure DevOps > Pipelines > Environments
2. “New environment” → İsim ver (`Staging`, `Prod`, `QA` vb.)
3. Ortam tipi seç: Kubernetes, VM, Azure Resource, None
4. Gerekirse kaynakları ekle (VM, Agent, Namespace, vb.)
5. Onaycılar ve güvenlik izinleri tanımla

---
## 📄 YAML ile Environment Kullanımı

```yaml
jobs:
- deployment: DeployToStaging
  displayName: 'Deploy to Staging'
  environment: 'Staging'
  strategy:
    runOnce:
      deploy:
        steps:
          - script: echo Deploying to staging!
```
---
## 🧪 Ortamda Onay & Denetim Mekanizması

- Ortama deploy etmeden önce `approver` zorunlu kılabilirsin.
- Ortam erişimini gruplara/kişilere kısıtlayabilirsin.
- Ortam bazlı denetim geçmişi saklanır.

---
## 🛡️ Ortam Güvenliği

- Ortama deploy edecek pipeline'a izin verilmelidir.
- Ortam içindeki kaynaklara erişim `RBAC` (role-based access control) ile sağlanır.
- Ortam bazlı onaycılar eklenebilir.

---
## 📊 Ortam İzleme Özellikleri

- Son deployment'lar
- Kimin ne zaman deploy ettiği
- Loglar ve çıktılar
- Başarı/başarısız geçmişi

---
## 💡 İpuçları

- Ortamları proje başında oluştur, her stage buna referans verir.
- Ortamda hangi pipeline’ların çalışabileceğini sınırlandır.
- Aynı ortamı farklı pipeline’lar için kullanarak merkezi kontrol sağla.

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/environments](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/environments)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/approvals](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/approvals)