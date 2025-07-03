# 📊 Monitoring with Grafana – Görsel Dashboard ve Veri Görselleştirme

## 🧠 Amaç

Farklı sistemlerden (Prometheus, Azure Monitor, Loki vb.) gelen verileri tek ekranda grafiklerle görselleştirmek için Grafana kurulumunu ve temel kullanımını öğrenmek.

---
## 🔍 Grafana Nedir?

- Zaman serisi veri kaynaklarına bağlanarak verileri görsel grafiklerle sunan açık kaynak bir izleme aracıdır.
- Prometheus, InfluxDB, ElasticSearch, Azure Monitor, Loki, PostgreSQL gibi birçok kaynağı destekler.
- Dashboard ve alert tanımları yapılabilir.

---
## 🛠️ Grafana Kurulumu (Kubernetes Üzerinde)

### 1. Helm ile Kurulum

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana
```
---
### 2. Admin Şifresi Öğrenme

```bash
`kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode`
```
### 3. Web Arayüzüne Erişim

```bash
`kubectl port-forward service/grafana 3000:80`
```

*Tarayıcıdan aç: `http://localhost:3000`*  
*Varsayılan kullanıcı: `admin` / (üstteki şifre)*

---
## 🔗 Veri Kaynağı Ekleme

### Örnek: Prometheus Bağlantısı

1. `Configuration > Data Sources > Add data source`
2. `Prometheus` seç
3. URL: `http://prometheus-server` (aynı namespace’te ise)
4. Save & Test → bağlantı başarılıysa dashboard'lara geçilebilir

---
## 📊 Dashboard Oluşturma

- Hazır dashboard şablonlarını https://grafana.com/grafana/dashboards üzerinden indirebilirsin.
- Örneğin: Kubernetes cluster metrikleri için `315` ID’li dashboard çok popülerdir.

### Dashboard ID ile Import

1. `+ > Import`
2. ID gir (örn: `315`)
3. Veri kaynağı olarak Prometheus seç

---
## 🧪 Alert Tanımlama

Grafana 8+ versiyonlarında alert tanımlama entegre olarak gelir.

- Panel > "Edit" > "Alert"
- Trigger: `avg CPU > 80` gibi bir koşul
- Notification: Slack, e-posta, webhook gibi hedefler eklenebilir

---
## 🧰 Kullanım Senaryoları

|Kaynak|Örnek Dashboard|
|---|---|
|**Prometheus**|Kubernetes pod durumu, CPU/memory|
|**Azure Monitor**|App Service response time|
|**Loki**|Log analizi (ELK alternatifi)|
|**PostgreSQL**|Query performansı, bağlantı sayısı|

---
## 💡 İpuçları

- Dashboard’ları JSON olarak dışa aktarabilir, sürüm kontrolü altında tutabilirsin.
- `Variables` kullanarak dinamik dashboard’lar oluşturabilirsin (örn: pod seçici).
- Kendi metriklerini Prometheus’a yollayarak Grafana’da izleyebilirsin.

---
## 🔗 Kaynaklar

- https://grafana.com/docs/grafana/latest/
- https://grafana.com/grafana/dashboards
- https://prometheus.io/docs/visualization/grafana/