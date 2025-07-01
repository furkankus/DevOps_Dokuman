# 💾 Kubernetes Persistent Volumes – Kalıcı Depolama Yönetimi

## 🧠 Amaç

Kubernetes pod’larının yaşam döngüsünden bağımsız olarak veri saklayabilmek için kalıcı depolama (Persistent Storage) kavramını öğrenmek.

---
## 🧱 Temel Kavramlar

| Terim              | Açıklama                                          |
|--------------------|--------------------------------------------------|
| **Persistent Volume (PV)**      | Fiziksel veya bulut tabanlı depolama kaynağı. Cluster tarafından sağlanır. |
| **Persistent Volume Claim (PVC)** | Kullanıcının PV’den belirli boyutta ve özellikte alan talebi. Pod’lar PVC üzerinden depolamaya bağlanır. |
| **Storage Class**   | Dinamik PV oluşturmak için tanımlanan depolama sınıfı. |

---
## 🔧 Persistent Volume Örneği
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-example
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```
### 🔧 Persistent Volume Claim Örneği
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-example
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```
### 📌 Pod’da Volume Kullanımı
```yaml
spec:
  containers:
    - name: my-container
      image: nginx
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: storage
  volumes:
    - name: storage
      persistentVolumeClaim:
        claimName: pvc-example
```
## 📄 Access Modes (Erişim Modları)

| Mod                 | Açıklama                           |
| ------------------- | ---------------------------------- |
| ReadWriteOnce (RWO) | Bir node’dan okuma-yazma           |
| ReadOnlyMany (ROX)  | Birden fazla node’dan sadece okuma |
| ReadWriteMany (RWX) | Birden fazla node’dan okuma-yazma  |
### 🔧 Storage Class Örneği (Dinamik PV için)
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
  fsType: ext4
```
## 💡 İpuçları

- Dinamik PV, StorageClass ile otomatik PV oluşturmayı sağlar.
- HostPath sadece test amaçlıdır, prod ortamda kullanılmaz.
- PVC, pod’dan bağımsızdır; pod silinse bile veri korunur.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/storage/persistent-volumes/
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/
