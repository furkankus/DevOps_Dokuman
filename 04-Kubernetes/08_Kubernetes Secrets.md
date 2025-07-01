# 🔐 Kubernetes Secrets – Hassas Bilgi Yönetimi

## 🧠 Amaç

Kubernetes ortamında şifre, token, sertifika gibi hassas bilgilerin güvenli ve yönetilebilir biçimde saklanmasını ve kullanılmasını öğrenmek.

---
## 🔑 Secret Nedir?

- Şifreler, API anahtarları, TLS sertifikaları gibi gizli bilgileri tutan Kubernetes nesnesi.
- Base64 formatında saklanır, ancak şifrelenmez (gizlilik sağlar ama tam güvenlik için ek yöntemler gerekir).
- Pod’lara güvenli şekilde aktarılır.

---
## 🔧 Secret Türleri

| Tür           | Açıklama                           |
|---------------|----------------------------------|
| Opaque        | Genel amaçlı, base64 kodlanmış veriler |
| docker-registry | Docker registry kimlik bilgileri için özel tür |
| tls           | TLS sertifikası ve anahtarı için kullanılır |

---
## 🔧 Secret Oluşturma Yöntemleri

### Komutla
```bash
kubectl create secret generic my-secret \
  --from-literal=username=admin \
  --from-literal=password=pass123
```
### YAML ile
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: YWRtaW4=       # base64(admin)
  password: cGFzczEyMw==   # base64(pass123)
```
*Base64 kodlama için:* **`echo -n 'admin' | base64`**
## 🔗 Secret Kullanımı Pod İçinde
### Ortam Değişkeni Olarak
```yaml
env:
  - name: USERNAME
    valueFrom:
      secretKeyRef:
        name: my-secret
        key: username
  - name: PASSWORD
    valueFrom:
      secretKeyRef:
        name: my-secret
        key: password
```
### Volume Olarak Mount Etmek
```yaml
volumes:
  - name: secret-volume
    secret:
      secretName: my-secret

volumeMounts:
  - name: secret-volume
    mountPath: "/etc/secret"
    readOnly: true
```
# 🔍 Secret Yönetimi Komutları
```bash
kubectl get secrets
kubectl describe secret my-secret
kubectl delete secret my-secret
kubectl get secret my-secret -o yaml
```
## 💡 İpuçları

- Secrets’ları doğrudan versiyon kontrol sistemine koymaktan kaçının.
- Daha gelişmiş güvenlik için **Sealed Secrets**, **HashiCorp Vault** gibi çözümler tercih edilir.
- Kubernetes 1.13 ve sonrası için encryption at rest (disk şifreleme) aktif edilebilir.
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/configuration/secret/
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-secret/
