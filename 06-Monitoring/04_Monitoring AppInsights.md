# 🔍 Application Insights – Uygulama İçin Telemetri ve İzleme

## 🧠 Amaç

Application Insights ile bir uygulamanın hata oranı, response time, kullanıcı davranışları ve performans ölçümlerini izlemeyi öğrenmek.

---
## 📌 Application Insights Nedir?

- Azure Monitor ailesine bağlı bir servistir.
- Uygulamanın içine gömülen SDK ile kullanıcı işlemlerinden exception’lara kadar çok detaylı veri toplar.
- Hem frontend (JS), hem backend (Node.js, .NET, Java vb.) destekler.

---
## 🧱 İzlenebilen Veriler

| İzleme Alanı     | Örnek Veriler |
|------------------|----------------|
| **Request**       | Endpoint bazlı istek sayısı, yanıt süresi |
| **Failure**       | Exception detayları, call stack |
| **Dependency**    | Veritabanı, HTTP, üçüncü parti API çağrıları |
| **User Behavior** | Hangi sayfalar ziyaret edildi, kullanıcı nerede çıktı |
| **Live Metrics**  | Anlık performans, CPU, bellek, istek akışı |

---
## ⚙️ Kurulum Yöntemleri

### 1. Azure Portal Üzerinden

- Azure Portal > “Application Insights” > “Create”
- App Service ile bağlamak için: App Service > Application Insights > Turn On

### 2. Kod İçine SDK Entegrasyonu

**.NET Core için:**

```bash
dotnet add package Microsoft.ApplicationInsights.AspNetCore
```

```csharp
// Program.cs içinde
builder.Services.AddApplicationInsightsTelemetry("<InstrumentationKey>");
```
**Node.js için**:
```bash
npm install applicationinsights
```

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<InstrumentationKey>").start();
```
---
## 🧪 Kullanışlı Özellikler

|Özellik|Açıklama|
|---|---|
|**Live Metrics**|Uygulamanın anlık trafik ve metrik akışı|
|**Failures**|Hataların exception tipi, satır no, kullanıcı bilgisi|
|**Performance**|Hangi endpoint ne kadar sürede yanıt veriyor|
|**Usage**|Sayfa görüntüleme, kullanıcı oturumu|
|**Smart Detection**|Azure’ın kendi önerileri ve uyarıları|

---
## 🔎 KQL ile Log Sorgulama

*Application Insights verileri Azure Monitor > Logs bölümünden sorgulanabilir.*

```kql
// En çok zaman alan endpoint'ler
requests
| summarize avg(duration) by name
| top 5 by avg_duration desc
```

```kql
// Hata nedenleri
exceptions
| summarize count() by type, outerMessage
```

---
## 💡 İpuçları

- Frontend JS uygulamaları için kullanıcı davranışı analizi de yapılabilir.
- Log’lar Azure Monitor Logs içinde saklanır, birleşik sorgular mümkündür.
- Anormal artış, response time dalgalanması gibi durumlar “Smart Detection” ile otomatik algılanır.

---

## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview](https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/app/asp-net-core](https://learn.microsoft.com/en-us/azure/azure-monitor/app/asp-net-core)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/app/nodejs](https://learn.microsoft.com/en-us/azure/azure-monitor/app/nodejs)