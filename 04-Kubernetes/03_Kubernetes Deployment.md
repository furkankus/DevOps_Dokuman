# 🚀 Kubernetes Deployment – Uygulama Dağıtımı

## 🧠 Amaç

Kubernetes ortamında uygulamaları **yönetilebilir**, **ölçeklenebilir** ve **güncellenebilir** şekilde dağıtmayı öğrenmek.

---
## 🧱 Deployment Nedir?

- **Deployment**, belirli bir container image’ini, istenen sayıda pod ile çalıştırmak için kullanılır.
- **Self-healing** özelliği sayesinde pod düşerse otomatik yenisini oluşturur.
- **Rolling Update** sayesinde kesintisiz güncelleme sağlar.
- Geri dönüş (rollback) desteği sunar.
---
## 📄 Örnek Deployment YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```
## 🔍 Açıklamalar

|Alan|Anlamı|
|---|---|
|`replicas`|Kaç adet pod çalışacağını belirtir|
|`selector`|Bu deployment’ın hangi pod’ları yöneteceğini belirler|
|`template`|Pod şablonudur, içindeki container yapısını gösterir|
|`image`|Kullanılacak container imajı|
|`containerPort`|Uygulamanın dinlediği port|
## ⚙️ Deployment Yönetimi
```bash
kubectl apply -f deployment.yaml       # Deployment oluştur/güncelle
kubectl get deployments                # Deployment’ları listele
kubectl describe deployment <ad>       # Detaylı bilgi al
kubectl delete deployment <ad>         # Deployment sil
```
## 🔁 Güncelleme (Rolling Update)
```bash
kubectl set image deployment/web-deployment nginx-container=nginx:1.21
```
- Yeni image ile pod’lar yavaşça güncellenir.
- Uygulama çalışmaya devam eder.
## 🔙 Rollback (Geri Dön)
```bash
kubectl rollout undo deployment/web-deployment
```
*Yeni versiyon sorun çıkarırsa eski sürüme dönmek için kullanılır.*
## 🔎 Dağıtım Durumu Takibi
```bash
kubectl rollout status deployment/web-deployment
```
*kubectl rollout status deployment/web-deployment*
## ⬆️ Deployment vs ReplicaSet vs Pod

|Kaynak|Görevi|
|---|---|
|**Pod**|Uygulamanın çalıştığı en küçük birim|
|**ReplicaSet**|Belirtilen sayıda pod’u ayakta tutar|
|**Deployment**|ReplicaSet’in versiyonlarını, geçişini, rollback’ini yönetir|
## 💡 Tavsiyeler

- Direkt pod kullanmak yerine **Deployment** kullanmak daha yönetilebilirdir.
- `labels` ve `selectors` doğru eşleştirilmelidir, yoksa Deployment pod’ları yönetemez.
- Her yeni versiyon değişikliğinde `kubectl rollout history` komutu ile geçmiş izlenebilir.
---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- https://kubernetes.io/docs/tasks/manage-deployment/