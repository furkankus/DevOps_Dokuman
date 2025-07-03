# 🧾 Monitoring with Log Analytics – Azure Log Analiz Platformu

## 🧠 Amaç

Azure'da çalışan sistemlerden gelen logları sorgulamak, analiz etmek ve anlamlı bilgiler çıkarmak için Log Analytics'i öğrenmek.

---
## 🔍 Log Analytics Nedir?

- Azure Monitor ve Application Insights ile entegre çalışan bir log analiz motorudur.
- Tüm Azure servislerinin diagnostik loglarını merkezi olarak depolar.
- KQL (Kusto Query Language) ile gelişmiş sorgular yazılabilir.

---
## 📌 Log Analytics ile Neler İzlenir?

| Kaynak               | Örnek Veri |
|----------------------|------------|
| Azure VM             | CPU, RAM, disk logları |
| Azure App Service    | HTTP istek logları, response time |
| AKS (Kubernetes)     | Pod logları, event’ler |
| Application Insights | Exception, request, dependency verisi |

---
## 🛠️ Log Analytics Workspace Kurulumu

1. Azure Portal → “Log Analytics Workspace” → Create
2. Workspace adı, kaynak grubu ve bölge belirle
3. İzlenecek kaynakları bu Workspace’e bağla (örn: App Service, AKS)

---
## 🔎 KQL – Kusto Query Language Temelleri

### 1. En Basit Örnek

```kql
Heartbeat
| take 10
```
*Son 10 heartbeat (canlılık sinyali) kaydını getirir.*

---
### 2. Azure App Service Response Time

```kql
requests 
| summarize avg(duration) by bin(timestamp, 5m)
```

### 3. Exception Dağılımı

```kql
exceptions 
| summarize count() by type, outerMessage
```

### 4. CPU Kullanımı Zamanla
```kql
Perf 
| where ObjectName == "Processor" and CounterName == "% Processor Time" 
| summarize avg(CounterValue) by bin(TimeGenerated, 5m), Computer
```
---
## 🔔 Alert Tanımlama (Log Tabanlı)

1. Log Analytics > Logs bölümünde sorgunu yaz
2. Sağ üstten "New Alert Rule" butonuna tıkla
3. Koşul ve eylem grubu (email, Teams, webhook vb.) tanımla
4. Otomatik tetiklenebilir hale gelir

---
## 📊 Dashboard Entegrasyonu

- Sorguları “Pin to Dashboard” ile ana Azure paneline ekleyebilirsin.
- Graf ve tablo olarak sunulabilir.
- Workbooks ile daha zengin görselleştirme yapılabilir.

---
## 💡 İpuçları

- `bin()` fonksiyonu ile zaman gruplama yapılır.
- `summarize`, `count`, `avg`, `top`, `join` gibi SQL benzeri fonksiyonlar kullanılır.
- Application Insights ile birleştirildiğinde uçtan uca log analizi yapılabilir.
- Her sorgunun maliyeti düşüktür ama yine de gereksiz karmaşıklıktan kaçın.

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-overview](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-overview)
- [https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/logs/tutorial-query](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/tutorial-query)