# 🔐 Azure DevOps – Security (Güvenlik) Giriş

## 🧠 Amaç

Azure DevOps üzerinde güvenli bir yazılım yaşam döngüsü için gerekli erişim kontrolleri, gizli anahtar yönetimi, kimlik denetimi ve güvenli pipeline yapılandırmalarını öğrenmek.

---
## 🔍 Azure DevOps Güvenlik Bileşenleri

| Bileşen           | Açıklama |
|-------------------|----------|
| **Organization Level Security** | Tüm DevOps organizasyonuna erişimi yönetir |
| **Project Level Security**      | Belirli bir projeye kim erişebilir |
| **Repositories Security**       | Repo bazlı okuma, yazma, yönetim izinleri |
| **Pipeline Security**           | Pipeline çalıştırma ve düzenleme yetkileri |
| **Service Connections**         | Dış servislerle güvenli bağlantılar (Azure, Docker Hub, GitHub vs.) |
| **Variable Groups & Secrets**   | Pipeline değişkenleri ve gizli anahtarlar |

---
## 🧱 Erişim Kontrol Katmanları

1. **Organization > Users**
   - Kullanıcıları davet et, rollerini belirle
2. **Project > Teams**
   - Gruplara ayırarak erişimi kolay yönet
3. **Permissions**
   - Her seviyede (repo, build, environment) ayrı ayrı izinler atanabilir
   - Roller: Reader, Contributor, Admin

---
## 🔐 Secure Pipeline Pratikleri

| Pratik                          | Açıklama |
|----------------------------------|----------|
| **Gizli Değişkenler (Secrets)**     | Variable group içinde `Keep secret` olarak işaretlenmeli |
| **Service Connection RBAC**        | Azure servis bağlantıları sınırlı erişimle tanımlanmalı |
| **Environment Approval Checks**    | Canlıya çıkmadan önce manuel onay eklenmeli |
| **Pipeline Permissions**           | Kim hangi pipeline’ı çalıştırabilir veya düzenleyebilir kontrol edilmeli |
| **YAML içinde Password Hardcoding**| Kesinlikle kaçınılmalı, her zaman değişken kullanılmalı |

---
## 🧪 Örnek: Gizli Değişken Kullanımı

```yaml
variables:
  - group: prod-secrets

steps:
  - script: echo "Connecting to DB..."
    env:
      DB_PASSWORD: $(dbPassword)
```

*`dbPassword` variable’ı Variable Group içinde tanımlı ve “secret” olarak işaretlenmiş olmalı.*

---
## ⚠️ Güvenlik Riskleri ve Önlemler

| Risk                            | Önlem                                                |
| ------------------------------- | ---------------------------------------------------- |
| Secrets loglarda görünmesi      | Secure flag kullan, log çıkışını sansürle            |
| Geniş yetkili Service Principal | Least Privilege ilkesi uygula                        |
| Public repository erişimi       | IP sınırlamaları ve özel repo kullan                 |
| Kod içinde credential           | Git hook, SonarQube, Trivy gibi araçlarla tarama yap |

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/organizations/security/overview](https://learn.microsoft.com/en-us/azure/devops/organizations/security/overview)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/security](https://learn.microsoft.com/en-us/azure/devops/pipelines/security)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups)