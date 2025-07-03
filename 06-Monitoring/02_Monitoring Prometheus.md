# 📡 Monitoring with Prometheus – Kubernetes İzleme

## 🧠 Amaç

Kubernetes üzerinde çalışan sistemlerin metriklerini toplamak ve izlemek için Prometheus kurulumu ve temel yapılandırmalarını öğrenmek.

---
## 🔍 Prometheus Nedir?

- CNCF (Cloud Native Computing Foundation) tarafından desteklenen açık kaynak monitoring sistemidir.
- Kubernetes ile doğal uyumlu, metrik tabanlı veri toplar.
- Zaman serisi verileri saklar ve PromQL adlı sorgu diliyle analiz yapılabilir.

---
## 🛠️ Prometheus Kurulumu (Kubernetes)

### 1. Helm ile Kurulum

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus
```
*Bu komutlar **`prometheus`** adında bir namespace’e tüm bileşenleri kurar (server, alertmanager, node exporter, vs).*

---
### 2. Kurulum Sonrası
```bash
kubectl port-forward deploy/prometheus-server 9090
```
*Tarayıcıdan `http://localhost:9090` ile Prometheus arayüzüne eriş.*

---
## 🧾 Metrik Toplama Mantığı

Prometheus, hedeflerden (targets) HTTP üzerinden `metrics` endpoint'inden veri çeker (`/metrics`).

Örnek: `http://node-exporter:9100/metrics`

---
### 🔎 PromQL Örnekleri
```promql
# Pod'ların CPU kullanımı
rate(container_cpu_usage_seconds_total[1m])

# Belirli bir deployment için memory kullanımı
sum(container_memory_usage_bytes{pod=~"my-app-.*"})

# Pod restart sayısı
sum(kube_pod_container_status_restarts_total)
```
---
### 🧰 Alerting (Uyarı Tanımlama)

*Prometheus Alertmanager ile beraber çalışır.*

```yaml
groups:
- name: example
  rules:
  - alert: HighPodRestart
    expr: sum(kube_pod_container_status_restarts_total) > 3
    for: 2m
    labels:
      severity: warning
    annotations:
      summary: "Pod restart sayısı fazla!"
```
---
## 💡 İpuçları

- Node Exporter, Kube State Metrics gibi exporter’lar sayesinde tüm sistem gözlemlenebilir.
- Prometheus verileri Grafana ile görselleştirilebilir.
- Alertmanager Slack, e-mail, webhook gibi hedeflere bildirim gönderebilir.

---
## 🔗 Kaynaklar

- [https://prometheus.io/](https://prometheus.io/)
- [https://github.com/prometheus-operator/kube-prometheus](https://github.com/prometheus-operator/kube-prometheus)
- https://grafana.com/docs/grafana/latest/datasources/prometheus/