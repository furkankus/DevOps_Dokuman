# 🗓️ Kubernetes Scheduling – Pod Planlama ve Yerleştirme

## 🧠 Amaç

Podların hangi node üzerinde çalışacağını belirleyen Kubernetes scheduling mekanizmasını öğrenmek.

---
## 🔍 Scheduler Nedir?

- Kubernetes’in podları uygun node’lara atayan bileşeni.
- Kaynak durumları, node etiketleri, politikalar dikkate alınır.

---
## 🔧 Temel Planlama Kriterleri

| Kriter               | Açıklama                             |
|----------------------|------------------------------------|
| **Node Capacity**    | CPU, RAM gibi kaynak kullanılabilirliği |
| **Node Affinity**    | Podların belirli node’larda çalışması için kurallar |
| **Taints & Tolerations** | Belirli node’lara podların atanmasını engelleme veya izin verme |
| **Pod Affinity / Anti-Affinity** | Podların birlikte ya da ayrı node’larda çalışmasını sağlama |

---
## 📦 Node Affinity Örneği

```yaml
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd
```
---
## 🛠️ Taints & Tolerations Örneği
```bash
# Node tarafı:
kubectl taint nodes node1 key=value:NoSchedule
```
```yaml
# Pod tarafı (yaml):
spec:
  tolerations:
  - key: "key"
    operator: "Equal"
    value: "value"
    effect: "NoSchedule"
```
---
## 💡 İpuçları

- Taints & Tolerations ile node izolasyonu sağlanır.
- Affinity kuralları ile esnek planlama yapılabilir.
- Pod yerleşimi için bu özellikleri doğru kullanmak kritik.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/scheduling-eviction/
- https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/