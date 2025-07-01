# ⚖️ Kubernetes Autoscaling – Otomatik Ölçeklendirme

## 🧠 Amaç

Uygulama yüküne göre pod sayısını otomatik artırıp azaltarak kaynakları etkin kullanmak.

---
## 🧩 Autoscaling Türleri

| Tür                       | Açıklama                                    |
|---------------------------|---------------------------------------------|
| **Horizontal Pod Autoscaler (HPA)** | Pod sayısını CPU, bellek veya özel metriklere göre ayarlar. |
| **Vertical Pod Autoscaler (VPA)**   | Pod içindeki container kaynaklarını (CPU, RAM) otomatik ayarlar. |
| **Cluster Autoscaler**              | Cluster’daki node sayısını otomatik arttırır veya azaltır. |

---
## 🔧 Horizontal Pod Autoscaler Örneği
```bash
kubectl autoscale deployment my-app --cpu-percent=50 --min=2 --max=10
```
*Bu komut, `my-app` deployment’ının CPU kullanımı %50 üzerine çıkarsa pod sayısını 2 ile 10 arasında otomatik artırır.*
## 📄 HPA YAML Örneği
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```
## ⚙️ Vertical Pod Autoscaler

- Kaynak sınırlarını otomatik ayarlar.
- Özellikle statik kaynak tanımları zor olan uygulamalarda faydalı.

---
## 🛠️ Cluster Autoscaler

- Bulut sağlayıcılar ile entegre çalışır (AWS, GCP, Azure).
- Yetersiz kaynak varsa yeni node ekler, boş node’ları kaldırır.

---
## 💡 İpuçları

- Autoscaling için metrics-server cluster’a kurulmalıdır.
- Kaynak limitleri ve istekleri (requests, limits) doğru belirlenmeli.
- Aşırı ölçeklendirme ve ani iniş çıkışları önlemek için sınırlar konulmalı.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/
- [https://github.com/kubernetes/autoscaler](https://github.com/kubernetes/autoscaler)