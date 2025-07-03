# ✅ Azure DevOps – Approvals & Checks (Onaylar ve Denetimler)

## 🧠 Amaç

Pipeline’ların belirli aşamalarında manuel onay, otomatik koşullar ve ortam güvenliğini sağlamak için Azure DevOps’ta Approvals & Checks sistemini öğrenmek.

---
## 🔍 Nedir Bu “Approval & Checks”?

- Pipeline çalışırken belirli bir **ortama deploy** yapmadan önce manuel onay gerektirir.
- Ayrıca **koşullara bağlı olarak** otomatik durdurma veya onaylama işlemi yapılabilir.
- Prod ortamları gibi kritik alanlar için yaygın olarak kullanılır.

---
## 🛠️ Nasıl Tanımlanır?

### 1. Ortam (Environment) Üzerinden

1. Azure DevOps > Pipelines > **Environments**
2. Yeni bir ortam oluştur (örneğin `production`)
3. Ortam ayarlarına gir > **Approvals and Checks** > `+ Add check`
4. Aşağıdaki türlerden birini seç:

| Check Türü            | Açıklama |
|------------------------|----------|
| **Approvals**          | Belirli kullanıcı(lar) veya gruplardan manuel onay istenir |
| **Branch Control**     | Sadece belirli branch’ten deploy izni |
| **Business Hours**     | Belirli saat/dönem dışında deploy engeli |
| **Invoke Azure Function** | Harici doğrulama (örneğin kimlik kontrol) |
| **Required Template**  | Belirli pipeline template kullanımı zorunluluğu |

---
## 🧪 YAML Pipeline'da Ortam Kullanımı

```yaml
jobs:
- deployment: deployToProd
  environment: 'production'
  strategy:
    runOnce:
      deploy:
        steps:
        - script: echo "Deploying to PROD!"
```
*Burada `production` ortamı tanımlanmış olmalı ve Approval eklendiyse manuel onay olmadan geçilmez.*

---
## ✅ Approval Özellikleri

| Özellik                    | Açıklama                                          |
| -------------------------- | ------------------------------------------------- |
| **Multiple Approvers**     | Birden fazla kişi onay vermeli kuralı eklenebilir |
| **Auto-reject timeout**    | Belirli sürede onay gelmezse otomatik reddedilir  |
| **Justification required** | Onaylayan kişiden açıklama istenebilir            |
| **Email Notification**     | Onay talebi e-posta ile bildirilir                |

---
## 🧰 Kullanım Senaryoları

|Senaryo|Açıklama|
|---|---|
|**Prod Deploy Öncesi Onay**|Hatalı deploy'ları önlemek için son adımda manuel kontrol|
|**Gece Deploy Engeli**|23:00 – 08:00 arası otomatik olarak deploy engelleme|
|**Regülasyon Gereği Onay**|Finansal ve yasal gerekliliklerde insan onayı|
|**CI sonrası CD için şart**|Build tamamlandıktan sonra sadece test geçmişse onay süreci|

---
## 💡 İpuçları

- Ortamları YAML ile değil Portal üzerinden oluşturmak daha yönetilebilir.
- Onaylama işlemini mobil uygulama üzerinden de yapabilirsin.
- Ortamları ekip üyelerine göre böl (örn: QA, Staging, Production).

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/environments](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/environments)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/approvals](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/approvals)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/checks](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/checks)