# 🔒 Azure DevOps – Service Connections ile Güvenli Servis Bağlantıları

## 🧠 Amaç

Azure DevOps’un dış servislerle (Azure, Docker Hub, GitHub, AWS vb.) güvenli şekilde bağlantı kurmasını sağlayan Service Connection yapılarını öğrenmek.

---
## 🔍 Service Connection Nedir?

- Azure DevOps’un dış sistemlere erişebilmesini sağlayan tanımlamalardır.
- Örneğin bir pipeline'ın Azure kaynaklarına veya Docker Registry'ye bağlanması için kullanılır.
- Güvenli kimlik bilgisi saklar ve kullanıcıya özel RBAC (Role-Based Access Control) uygular.

---
## 🛠️ Desteklenen Servis Türleri

| Servis Türü     | Örnek |
|------------------|-------|
| **Azure Resource Manager** | Azure VM, App Service, Container Registry |
| **Docker Registry**        | Docker Hub, Azure Container Registry |
| **GitHub / Bitbucket**     | SCM erişimi |
| **Kubernetes**             | AKS cluster bağlantısı |
| **Generic**                | Kullanıcı tanımlı herhangi bir API / URL bağlantısı |

---
## ⚙️ Azure Service Connection Oluşturma

1. Azure DevOps Portal > Project Settings > Service connections
2. `+ New service connection` > Azure Resource Manager seç
3. Authentication yöntemi:
   - **Service principal (automatic):** En kolay ve önerilen yol
   - **Manual:** Mevcut service principal bilgileriyle
4. Ad ver > Gerekirse erişim kısıtlamaları ayarla

*“Grant access permission to all pipelines” seçeneği dikkatli kullanılmalı!*

---
## 🔑 Docker Hub Bağlantısı (Örnek)

1. `New service connection > Docker Registry`
2. Server URL: `https://index.docker.io/v1/`
3. Kullanıcı adı ve access token gir
4. Connection name: `docker-hub-conn`

Pipeline YAML örneği:

```yaml
resources:
  containers:
    - container: myimage
      image: myrepo/myimage:latest
      en
```
---
## 🔐 Güvenlik Pratikleri

| Güvenlik Alanı                  | Açıklama                                                                      |
| ------------------------------- | ----------------------------------------------------------------------------- |
| **Least Privilege**             | En az izinli SP kullanımı (Sadece ihtiyacı olan rol atanmalı)                 |
| **Pipeline Access Restriction** | Belirli pipeline’lara erişim izni verilmesi                                   |
| **Credential Rotation**         | Periyodik access key/token yenilemesi                                         |
| **Service Connection Approval** | Manual onay zorunluluğu ayarlanabilir                                         |
| **Connection Scopes**           | Organization ya da Project seviyesinde açılabilir, proje seviyesinde önerilir |

---
### 🧾 YAML Kullanımı
```yaml
jobs:
- deployment: deployWeb
  environment: staging
  pool:
    vmImage: 'ubuntu-latest'
  strategy:
    runOnce:
      deploy:
        steps:
        - task: AzureWebApp@1
          inputs:
            azureSubscription: 'my-azure-conn'
            appName: 'my-web-app'
            package: '$(System.DefaultWorkingDirectory)/drop/*.zip'
```
---
## 💡 İpuçları

- Birden fazla Service Connection tanımlayıp ortama göre seçim yapabilirsin (dev / prod).
- Azure CLI kullanarak da Service Connection oluşturulabilir.
- Service Connection erişimleri RBAC ile ayrı ayrı yönetilmelidir.

---

## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-deployment](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-deployment)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables)