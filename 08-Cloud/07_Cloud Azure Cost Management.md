# 💰 Azure Cloud – Cost Management ve Bütçe Takibi

## 🧠 Amaç

Azure kaynaklarının maliyetlerini yönetmek, bütçe sınırları belirlemek ve gereksiz harcamaları azaltmak.

---

## 📊 1. Azure Cost Management + Billing Nedir?

Azure’un maliyet takibi ve analiz servisidir.  
Kullanıcıya:
- Harcama izleme
- Bütçe belirleme
- Uyarılar alma
- Raporlama ve analiz
imkanları sunar.

---

## 📦 2. Bileşenler

| Bileşen             | Açıklama |
|---------------------|----------|
| **Cost Analysis**   | Kaynaklara göre harcama analizi |
| **Budgets**         | Aylık, yıllık veya özel dönemli bütçe limiti koyma |
| **Alerts**          | Bütçeye ulaşıldığında uyarı gönderme |
| **Recommendations** | Tasarruf önerileri sunar (örneğin kullanılmayan disk, düşük CPU’lu VM vs.) |

---

## 📌 3. Cost Analysis Kullanımı

Portal:  
🧭 Azure Portal → Cost Management + Billing → Cost analysis

Filtreleme:
- Kaynak grubu
- Abonelik
- Servis türü (örn: VM, Storage)
- Lokasyon
- Etiket (tag)

---

## 📅 4. Bütçe Tanımlama (Budget)

### Adımlar:
1. Aboneliği seç
2. “+ Add” ile bütçe oluştur
3. Miktar, zaman aralığı ve scope seç
4. Yüzde bazlı uyarı tanımla (örnek: %80’e ulaşınca e-posta gönder)

---

## 🔔 5. Alert Ayarlama

- Bütçe ile entegre çalışır
- Kullanıcıya e-posta ile bildirim yapılabilir
- Azure Action Groups ile Slack/Teams entegrasyonu yapılabilir

---

## 🧠 6. Azure Advisor ile Maliyet Optimizasyonu

Azure’un öneri servisidir. Aşağıdaki başlıklarda iyileştirme sunar:

| Kategori       | Örnek |
|----------------|-------|
| High Availability | Availability set eksik |
| Cost            | Kullanılmayan disk/VM |
| Performance     | Düşük bellekli VM uyarısı |
| Security        | Port açık, MFA yok vb. |

---
## 💡 7. Tasarruf Yöntemleri

| Yöntem                            | Açıklama |
|----------------------------------|----------|
| **Auto Shutdown (Dev/Test VM)** | Belirli saatlerde otomatik kapama |
| **Reserved Instances (RI)**      | 1-3 yıllık sabit VM kiralama (az ücret) |
| **Spot Instances**               | Uygun fiyatlı geçici VM’ler |
| **Azure Hybrid Benefit**         | Mevcut Windows lisanslarını kullanarak tasarruf |
| **Unattached Disk Clean-Up**     | Bağlı olmayan diskleri sil |

---
## 🧮 8. Tag’leme ile Takip

Azure kaynaklarını etiketleyerek (örneğin `env=dev`, `team=backend`) maliyet analizi yapılabilir.

```bash
az tag create \
  --name env \
  --values dev prod test
```
---
## 📉 9. Raporlama ve Dışa Aktarım

- CSV/PDF olarak dışa aktarım
- Power BI entegrasyonu
- REST API ile maliyet çekimi mümkündür

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/cost-management-billing/](https://learn.microsoft.com/en-us/azure/cost-management-billing/)
- [https://learn.microsoft.com/en-us/azure/advisor/](https://learn.microsoft.com/en-us/azure/advisor/)
- [https://azure.microsoft.com/en-us/pricing/](https://azure.microsoft.com/en-us/pricing/)