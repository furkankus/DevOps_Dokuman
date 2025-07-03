# 🔗 Azure DevOps Service Connections – Dış Sistemlerle Güvenli Bağlantı

## 🧠 Amaç

Azure DevOps içinde dış kaynaklara (Azure, Docker Hub, Kubernetes, GitHub vb.) güvenli bağlantılar kurarak deployment ve entegrasyon süreçlerini yönetmeyi öğrenmek.

---
## 🔍 Service Connection Nedir?

- Azure DevOps’un dış sistemlerle (Azure, AWS, Docker, GitHub, K8s, vs.) konuşabilmesi için oluşturulan güvenli bağlantılardır.
- Pipeline’ların dış kaynaklara erişmesi için kullanılır.

---
## 🧱 Yaygın Kullanılan Service Connection Türleri

| Tür                    | Açıklama |
|-------------------------|----------|
| **Azure Resource Manager (ARM)** | Azure portal kaynaklarına erişim |
| **Docker Registry**     | Docker Hub ya da Azure Container Registry erişimi |
| **Kubernetes**          | AKS veya manuel k8s erişimi |
| **GitHub / Bitbucket**  | Kod kaynaklarına bağlantı |
| **Generic / SSH / Username+Password** | Diğer özel sistemler için |

---
## 🛠️ Service Connection Nasıl Oluşturulur?

1. Azure DevOps > Project Settings > **Service Connections**
2. “New Service Connection” butonuna tıkla
3. Bağlantı türünü seç (örn. Azure Resource Manager)
4. Gerekli kimlik bilgilerini gir:
   - Azure için: Service Principal
   - Docker için: Docker kullanıcı adı & token
   - K8s için: kubeconfig bilgisi
5. Connection’a isim ver ve `Grant access permission to all pipelines` kutusunu işaretle

---
## 🔐 Güvenlik

- Servis bağlantılarına sadece yetkili pipeline'lar erişebilir.
- Dilersen bağlantıyı sadece belirli pipeline veya stage ile sınırlayabilirsin.
- "Manage Service Connections" yetkisi olan kullanıcılar tarafından düzenlenebilir.

---
## 📄 YAML'da Service Connection Kullanımı

### Azure'a deploy örneği:

```yaml
- task: AzureWebApp@1
  inputs:
    azureSubscription: 'MyAzureConnection'  # Service connection adı
    appName: 'my-web-app'
    package: '$(System.DefaultWorkingDirectory)/drop/app.zip'
```
---
### Docker push örneği:
```yaml
- task: Docker@2
  inputs:
    containerRegistry: 'MyDockerHubConnection'
    repository: 'my-app'
    command: 'push'
    tags: '$(Build.BuildId)'
```
---
## 📊 Yönetim ve İzleme

- Servis bağlantıları `Project Settings > Service Connections` altında listelenir.
- Hangi pipeline ne zaman kullanmış, kim oluşturmuş gibi loglar tutulur.
- Token süresi dolan bağlantılar için yenileme uyarıları alınabilir.

---
## 💡 İpuçları

- Bağlantı adlarını anlamlı ve ortama özgü koy: `Azure-Prod`, `K8s-Staging`, `DockerHub-Furkan`
- Paylaşılan bağlantılar yerine ortam özel bağlantılar kullanmak erişim kontrolünü artırır.
- Eğer bağlantı çalışmazsa pipeline loglarında hata detayları görülür.

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-deployment](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-deployment)