# 🧱 Kubernetes StatefulSets – Durumlu Uygulama Yönetimi

## 🧠 Amaç

Stateful (durumlu) uygulamaları Kubernetes üzerinde yönetmek için StatefulSet kaynak tipini öğrenmek.

---
## 🔍 StatefulSet Nedir?

- Stateful uygulamalar için podların sıra ve kalıcı kimlik gereksinimlerini karşılar.
- Her podun sabit bir kimliği (hostname ve kalıcı depolaması) olur.
- Örneğin veritabanları, mesaj kuyruğu sistemleri için idealdir.

---
## 🔧 StatefulSet Özellikleri

| Özellik                                                       | Açıklama                                  |
| ------------------------------------------------------------- | ----------------------------------------- |
| Pod sıralı oluşturma                                          | Pod’lar belirli bir sırayla başlatılır.   |
| Kalıcı kimlik                                                 | Her pod benzersiz ve sabit bir isim alır. |
| Kalıcı depolama                                               | PVC ile kalıcı depolama bağlanır.         |
| Pod yeniden başlatıldığında aynı isim ve depolama kullanılır. |                                           |

---
## 📦 StatefulSet Örneği

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.17
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```
## 🛠️ StatefulSet ile Hizmet Sağlama

- StatefulSet için bir Headless Service (clusterIP: None) oluşturulur.
- Podlar DNS üzerinden sabit isimlerle erişilir.

---
## 💡 İpuçları

- StatefulSet, replica set’ten farklı olarak durum yönetimi için kullanılır.
- Yatay ölçeklendirme sırasında dikkatli olunmalı, bazı uygulamalar sıraya ihtiyaç duyar.
- PVC kullanımı ile veri kaybı önlenir.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/
- https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/
