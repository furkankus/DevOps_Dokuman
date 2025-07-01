# 📝 Kubernetes Logging – Log Yönetimi ve Analizi

## 🧠 Amaç

Kubernetes cluster’ında çalışan uygulamaların ve altyapının loglarını toplayıp merkezi şekilde yönetmeyi öğrenmek.

---
## 🔍 Neden Log Yönetimi Önemli?

- Hata tespiti ve troubleshooting
- Performans analizi
- Güvenlik incelemeleri
- Sistem davranışlarının takibi

---
## 🛠️ Popüler Log Yönetim Araçları

| Araç                    | Açıklama                         |
|-------------------------|---------------------------------|
| **Elasticsearch (ES)**  | Logların depolanması ve sorgulanması |
| **Fluentd / Fluent Bit**| Log toplayıcı ajanlar            |
| **Kibana**              | Logların görselleştirilmesi      |
| **Loki (Grafana Loki)** | Log toplama ve Grafana ile entegrasyon |

---
## 📦 EFK Stack Kurulumu (Örnek)

- Elasticsearch + Fluentd + Kibana kombinasyonu
- Fluentd logları toplar, Elasticsearch depolar, Kibana görselleştirir

---
## 🔧 Fluentd DaemonSet Örneği

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
  namespace: kube-system
spec:
  selector:
    matchLabels:
      name: fluentd
  template:
    metadata:
      labels:
        name: fluentd
    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd:v1.14
        resources:
          limits:
            memory: 200Mi
          requests:
            cpu: 100m
            memory: 200Mi
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibdockercontainers
          mountPath: /var/lib/docker/containers
          readOnly: true
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibdockercontainers
        hostPath:
          path: /var/lib/docker/containers
```
## 📚 Log Toplama Yaklaşımları

- **DaemonSet** ile her node’dan log topla
- Uygulama içinde log dosyası veya stdout/stderr kullanımı
- Merkezi log toplama sistemine gönderim

---
## 💡 İpuçları

- Log seviyelerini doğru ayarla (INFO, WARN, ERROR)
- Log miktarını kontrol et, disk alanını yönet
- Loglarda hassas bilgi olmamasına dikkat et

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/cluster-administration/logging/
- [https://www.elastic.co/what-is/elk-stack](https://www.elastic.co/what-is/elk-stack)
- https://grafana.com/oss/loki/