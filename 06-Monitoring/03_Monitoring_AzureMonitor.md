# 🧭 Azure Monitor – Azure Kaynak İzleme

## 🧠 Amaç

Azure üzerinde çalışan sanal makineler, app services, container’lar gibi kaynakları gerçek zamanlı izlemek, loglamak ve uyarılar tanımlamak için Azure Monitor’ü kullanmayı öğrenmek.

---
## 🔍 Azure Monitor Nedir?

- Azure üzerinde çalışan kaynakların performans, sağlık ve güvenlik durumunu gözlemlemeye yarayan kapsamlı bir izleme çözümüdür.
- Telemetri toplar, analiz eder ve gerektiğinde alert üretir.

---
## 🧱 İzlenen Kaynaklar

| Kaynak            | İzlenen Veriler |
|-------------------|-----------------|
| VM                | CPU, RAM, Disk, Ağ kullanımı |
| Azure App Service | HTTP istekleri, Hata oranı, Yanıt süresi |
| AKS (Kubernetes)  | Pod durumu, Node sağlığı, HPA metrikleri |
| Azure SQL         | Query performansı, CPU, I/O |

---
## 🛠️ Azure Monitor Bileşenleri

| Bileşen             | Görev |
|----------------------|------|
| **Metrics**          | Sayısal performans verileri |
| **Logs**             | Diagnostik ve olay log’ları (KQL ile sorgulanır) |
| **Alerts**           | Kural tabanlı uyarı mekanizması |
| **Dashboards**       | Grafik tabanlı gösterim |
| **Workbooks**        | Raporlama ve görselleştirme |
| **Insights**         | Servis özel analiz ekranları (örn: VM Insights, App Insights) |

---
## 🧪 Azure Monitor Nasıl Kullanılır?

### 1. Azure Portal > Monitor

- “Metrics” sekmesinden kaynak seç → metrik belirle → grafik çiz
- “Logs” sekmesinde KQL (Kusto Query Language) ile sorgu yap

### 2. Uyarı (Alert) Tanımlama

1. Azure Monitor > Alerts > “New alert rule”
2. Kaynak seç (örn: App Service)
3. Koşul belirle (örn: `CPU % > 80`)
4. Eylem grubu oluştur (örn: e-posta gönder)
5. Alert kuralını kaydet

---
## 🔍 Örnek KQL Sorguları

```kql
// App Service response time'larını getir
requests
| summarize avg(duration) by bin(timestamp, 5m)

// CPU % kullanımını göster
Perf
| where CounterName == "% Processor Time"
| summarize avg(CounterValue) by bin(TimeGenerated, 5m), Computer
```
---
## 💡 İpuçları

- App Service, AKS, Function App gibi servisler için özel “Insights” panelleri vardır.
- Alert geçmişini takip edebilir, çözüm adımlarını kaydedebilirsin.
- Metrics Explorer ile kendi dashboard’ını oluşturabilirsin.

---

## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/azure-monitor/](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-platform](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-platform)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-queries](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-queries)