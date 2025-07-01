# 📊 Kubernetes Monitoring – İzleme ve Performans Takibi

## 🧠 Amaç

Kubernetes ortamını ve uygulamalarını izleyerek performans sorunlarını erken tespit etmek ve sistem sağlığını takip etmek.

---
## 🔍 İzleme Neden Önemli?

- Pod ve node sağlık durumu
- Kaynak kullanımı (CPU, RAM, disk)
- Uygulama performansı ve loglar
- Hata ve uyarıların hızlı tespiti

---
## 🛠️ Popüler İzleme Araçları

| Araç            | Açıklama                                  |
|-----------------|-------------------------------------------|
| **Prometheus**  | Metric toplama ve sorgulama aracı         |
| **Grafana**     | Görselleştirme ve dashboard oluşturma     |
| **Kube-state-metrics** | Kubernetes kaynaklarından metrik toplama  |
| **Elasticsearch + Fluentd + Kibana (EFK)** | Log toplama ve analiz      |

---
## 📦 Prometheus Kurulumu Örneği
```bash
kubectl create namespace monitoring
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus --namespace monitoring
```
## 📈 Grafana ile Dashboard

- Prometheus’tan veri alır.
- Hazır dashboardlar ile hızlıca görselleştirme sağlar.

---

## 🔧 Metrik Toplama

- Pod ve node metrikleri `kube-state-metrics` ve `node-exporter` ile toplanır.
- Kendi uygulaman için Prometheus client kütüphaneleri kullanarak özel metrik ekleyebilirsin.
## 📊 İzleme Komutları
```bash
kubectl get pods -n monitoring
kubectl logs <pod-adı> -n monitoring
```
## 💡 İpuçları

- İzleme sistemleri yüksek kaynak tüketebilir, kapasite planlaması yap.
- Kritik metrikler için alert kur.
- Log ve metrikleri ayrı tutup analiz etmek faydalıdır.

---

## 🔗 Kaynaklar

- https://prometheus.io/docs/introduction/overview/
- https://grafana.com/docs/
- https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/