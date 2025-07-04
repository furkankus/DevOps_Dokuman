# 📡 Azure Cloud – İzleme ve Loglama (Monitoring & Logging)

## 🧠 Amaç

Azure ortamında uygulama ve altyapı kaynaklarını izlemek, log toplamak ve uyarı mekanizmalarını kurmak.

---
## 🔍 1. Azure Monitor Nedir?

Azure kaynaklarının **performans, sağlık ve kullanılabilirlik durumunu** izlemek için kullanılan merkezi izleme servisidir.

### Özellikler:
- Metric ve Log verilerini toplar
- Uyarılar oluşturur
- Dashboard ve grafikler sunar
- Diğer hizmetlerle entegredir (Log Analytics, Alerts, App Insights)

---
## 📊 2. Log Analytics

Azure kaynaklarından gelen log'ları toplayan ve Kusto Query Language (KQL) ile analiz edilebilen platform.

### Başlıca Log Kaynakları:
- VM’ler (agent ile)
- Azure Resource Logs
- App Insights verileri
- NSG, AKS, Function logları

### Örnek Sorgu:

```kql
AzureActivity
| where ActivityStatus == "Failed"
| summarize count() by ResourceGroup
```
---
## 📦 3. Application Insights

Web uygulamaları için:

- Performans izleme
- Hata takibi
- Kullanıcı davranışları
- Live Metrics akışı sağlar
```bash
az monitor app-insights component create \
  --app myAppInsights \
  --location westeurope \
  --resource-group myRG \
  --application-type web
```
---
## ⏱️ 4. Metrics Explorer

- CPU, Disk, Memory gibi sistemsel metrikleri izleme
- Grafiksel dashboard oluşturma
- Threshold ile uyarı tetikleme

---
## 🚨 5. Alerts (Uyarılar)

Belirli bir koşul gerçekleştiğinde e-posta, SMS, webhook veya otomasyon tetikler.

### Adımlar:

1. Kaynağı seç (VM, App Service, AKS vb.)
2. Koşul tanımla (örn: CPU > 90%)
3. Action Group belirle (e-posta, script, webhook vs.)
```bash
az monitor metrics alert create \
  --name HighCPUAlert \
  --resource-group myRG \
  --scopes /subscriptions/<id>/resourceGroups/myRG/providers/Microsoft.Compute/virtualMachines/myVM \
  --condition "avg Percentage CPU > 90" \
  --window-size 5m \
  --evaluation-frequency 1m \
  --action-group myActionGroup
```
---
## 🛠️ 6. Diagnostic Settings

Her Azure hizmeti için log’ların:

- Log Analytics’e,
- Event Hub’a,
- Storage Account’a yönlendirilmesini sağlar.
```bash
az monitor diagnostic-settings create \
  --name diagForVM \
  --resource <resource-id> \
  --workspace <log-analytics-id>
```
---
## 📈 7. Workbook ile Görselleştirme

- Dashboard'lar oluşturmak için kullanılır
- Sürükle bırak yöntemiyle grafik, tablo vs.
- Ortamın sağlığı kolay takip edilebilir

---
## 🌐 8. Entegrasyonlar

|Sistem|Entegrasyon|
|---|---|
|**Azure DevOps**|Build/deploy izleme|
|**Grafana**|Azure Monitor plugin ile veri çekimi|
|**Power BI**|Raporlama|
|**Event Grid**|Gerçek zamanlı event notification|

---
## 🔐 Güvenlik & Uygulama

- Uyarılara RBAC uygulanabilir
- Veriler Log Analytics Workspace ile merkezi olarak toplanır
- Role atamaları ile erişim kontrolü sağlanır

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/azure-monitor/](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/logs/](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/)    
- [https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview](https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview/)