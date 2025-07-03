# 🛑 Azure DevOps Approvals – Onay ve Müdahale Süreçleri

## 🧠 Amaç

Release ve deployment süreçlerinde kullanıcıdan onay alma, duraklatma ve manuel müdahale noktaları eklemeyi öğrenmek.

---
## 🔍 Approvals Nedir?

- Deployment işlemlerinin belirli aşamalarında **insan müdahalesi** veya **onay** gerektiren adımlardır.
- Genellikle staging → production gibi kritik geçişlerde kullanılır.

---
## 🧱 Onay Mekanizması Türleri

| Tür                       | Açıklama |
|---------------------------|----------|
| **Pre-deployment approval** | Ortama deploy başlamadan önce onay istenir |
| **Post-deployment approval**| Deploy tamamlandıktan sonra onay alınır (örneğin: sonraki aşamaya geçmeden önce) |
| **Manual Intervention**     | Ortamda bir şey kontrol edilip elle onay verilmesi gereken durumlarda kullanılır |

---
## ⚙️ UI Üzerinden Approval Ayarı

1. Azure DevOps > Pipelines > Releases
2. Release Pipeline > Stage > "Pre-deployment conditions"
3. "Pre-deployment approvals" alanına kullanıcı veya grup ekle
4. Gerekirse "timeout" veya "approval timeout notification" tanımla

---
## 🔒 Güvenlik & Rollerin Önemi

- Yalnızca yetkili kişilerin onay verebilmesi için kullanıcı/grup seçimi önemlidir.
- Örn: QA onayı olmadan staging'e deploy yapılmasın.

---
## 🛠️ Manual Intervention Örneği

Release pipeline’a şu şekilde bir manuel müdahale adımı eklenebilir:

```yaml
- task: ManualValidation@0
  inputs:
    instructions: 'Uygulama doğru çalışıyor mu? Devam etmek için onay verin.'
    onTimeout: 'reject'
    timeout: '1h'
```
*YAML pipeline’larında bu task `stage` veya `job` seviyesinde duraklama sağlar.*

---
## 🔁 Onay Sürecinin Avantajları

- Kritik ortamlarda güvenliği artırır.
- İnsan hatasına karşı kontrol sağlar.
- Ekip içinde sorumluluk paylaşımını düzenler.

---
## 💡 İpuçları

- Production geçişlerinden önce her zaman onay alınması önerilir.
- Birden fazla onaycı eklenebilir → çoğunluk/onay gereksinimi ayarlanabilir.
- Süre dolduğunda otomatik red veya onay seçilebilir (`onTimeout` parametresi).

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/approvals](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/approvals)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/manual-validation](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/manual-validation)