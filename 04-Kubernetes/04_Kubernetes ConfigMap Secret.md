# ⚙️ ConfigMap ve Secret – Ayar ve Güvenli Bilgi Yönetimi

## 🧠 Amaç

Uygulamaların ortam ayarlarını ve hassas bilgilerini Pod dışında yönetmeyi öğrenmek.

---
## 📦 ConfigMap Nedir?

- Ortam değişkenleri, yapılandırma dosyaları, komut satırı parametreleri gibi **hassas olmayan ayarları** Pod'lara dışarıdan geçmek için kullanılır.

---
## 🗂️ ConfigMap Oluşturma Yolları

### 1. Komutla
```bash
kubectl create configmap app-config \
  --from-literal=APP_MODE=production \
  --from-literal=APP_PORT=8080
```
### 2. YAML ile
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_MODE: production
  APP_PORT: "8080"
```
# 🔗 Pod İçinde Kullanma

### 1. Ortam Değişkeni Olarak
```yaml
env:
  - name: APP_MODE
    valueFrom:
      configMapKeyRef:
        name: app-config
        key: APP_MODE
```
### 2. Tümünü Otomatik Alma
```yaml
envFrom:
  - configMapRef:
      name: app-config
```
## 🔐 Secret Nedir?

- **Şifre**, **API anahtarı**, **veritabanı kullanıcı bilgisi** gibi hassas verileri saklar.
- Base64 ile encode edilir (şifrelenmez ama gizlenir).
- Pod’lara güvenli şekilde aktarılır.
# 🔐 Secret Oluşturma Yolları
### 1. Komutla
```bash
kubectl create secret generic db-secret \
  --from-literal=DB_USER=admin \
  --from-literal=DB_PASS=sifre123
```
### 2. YAML ile
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  DB_USER: YWRtaW4=       # base64(admin)
  DB_PASS: c2lmcmUxMjM=   # base64(sifre123)
```
*Base64 çevrimi için:* **`echo -n 'admin' | base64`**
## 🔗 Secret’ı Pod’da Kullanmak
### 1. Ortam Değişkeni Olarak
```yaml
env:
  - name: DB_USER
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: DB_USER
```
### 2. Volume Olarak Mount Etmek
```yaml
volumes:
  - name: secret-volume
    secret:
      secretName: db-secret

volumeMounts:
  - name: secret-volume
    mountPath: "/etc/secrets"
    readOnly: true
```
## 🔎 Secret ve ConfigMap Karşılaştırması

|Özellik|ConfigMap|Secret|
|---|---|---|
|Amaç|Ortam ayarları|Şifre, token, anahtar|
|Şifreli mi?|❌ Hayır|🔒 Base64 (gizli ama şifreli değil)|
|Volumeye takılabilir mi?|✅ Evet|✅ Evet|
|Ortam değişkeni yapılabilir mi?|✅ Evet|✅ Evet|
# 🛠️ Kontrol Komutları
```bash
kubectl get configmaps
kubectl describe configmap app-config

kubectl get secrets
kubectl describe secret db-secret
kubectl get secret db-secret -o yaml
```
## 🧠 İpuçları

- **ConfigMap** = ayar; **Secret** = hassas bilgi
- Secret’ları versiyon kontrol sistemine (Git) koyma
- Base64 şifreleme değildir, sadece gizleme sağlar. Ek şifreleme için Sealed Secrets veya External Secrets operatörleri kullanılabilir.
---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/configuration/configmap/
- https://kubernetes.io/docs/concepts/configuration/secret/