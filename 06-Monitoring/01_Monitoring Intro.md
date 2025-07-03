# 📈 Monitoring – Uygulama ve Altyapı İzleme Giriş

## 🧠 Amaç

Sistemlerin ve uygulamaların performans, sağlık, hata ve kaynak kullanım durumlarının sürekli izlenmesi için monitoring temellerini öğrenmek.

---
## 🔍 Monitoring Nedir?

- Sistemin anlık ve geçmiş durumunu gözlemlemeye yarar.
- Uygulama, konteyner, node, veri tabanı gibi bileşenlerin performansı izlenir.
- Anormallikler, hatalar ve uyarılar gerçek zamanlı yakalanabilir.

---
## 🎯 Neden Önemlidir?

| Neden             | Açıklama |
|--------------------|----------|
| **Erken uyarı**     | Sorunlar büyümeden tespit edilir. |
| **Performans analizi** | Tıkanma noktaları ve darboğazlar belirlenir. |
| **Log analizi**     | Hataların kök nedenine ulaşılır. |
| **Otomatik tepki**  | Alert’lerle otomatik aksiyonlar alınabilir (örneğin pod restart). |

---
## 🔧 İzlenecek Katmanlar

| Katman              | İzlenecek Veriler |
|---------------------|-------------------|
| **Uygulama**        | Response time, error rate, request count |
| **Container**       | CPU, memory, restart count, I/O |
| **Kubernetes**      | Pod health, node status, deployment state |
| **Veri tabanı**     | Query time, connection pool, replication |
| **Donanım/VM**      | Disk, RAM, CPU, Network I/O |

---
## 🧰 Yaygın Monitoring Araçları

| Araç         | Açıklama |
|--------------|----------|
| **Prometheus** | Kubernetes monitoring için en yaygın çözümlerden biri |
| **Grafana**    | Prometheus verilerini görselleştirmek için |
| **Azure Monitor** | Azure kaynakları için yerleşik izleme |
| **Application Insights** | Uygulama performansını ve hataları izlemek için |
| **ELK Stack (Elasticsearch, Logstash, Kibana)** | Log tabanlı izleme |
| **Datadog / New Relic** | SaaS tabanlı izleme çözümleri |

---
## ⚙️ İzleme ile Neleri Yapabilirim?

- Otomatik uyarı ve aksiyon tanımlama (örneğin: CPU %90’ı geçerse Slack’e mesaj gönder)
- Dashboard'larla sistem sağlığını görselleştirme
- Otomatik scale kararlarını destekleme (Horizontal Pod Autoscaler)
- Sorun anında root cause (kök neden) tespiti yapma

---
## 💡 İpuçları

- Kubernetes kullanıyorsan Prometheus + Grafana kurulumu standarttır.
- Azure Web App kullanıyorsan Application Insights entegresi birkaç tıkla yapılır.
- İzleme verilerini hem canlı (real-time) hem de geçmişe dönük tutmak önemlidir.

---
## 🔗 Kaynaklar

- [https://grafana.com/](https://grafana.com/)
- [https://prometheus.io/](https://prometheus.io/)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/](https://learn.microsoft.com/en-us/azure/azure-monitor/)
- [https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview](https://learn.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview)
