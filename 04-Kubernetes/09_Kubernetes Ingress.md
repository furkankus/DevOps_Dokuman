# 🌐 Kubernetes Ingress – Dış Trafik Yönetimi ve Yönlendirme

## 🧠 Amaç

Kubernetes cluster’ına dış dünyadan gelen HTTP/HTTPS trafiğini yönetmek ve farklı servisleri tek IP altında yönlendirmek.

---
## 🧩 Ingress Nedir?

- HTTP ve HTTPS trafiğini servisler arasında yönlendiren kaynak.
- Tek bir dış IP üzerinden birden çok servise erişim sağlar.
- Yönlendirme kurallarını (host, path bazlı) tanımlar.

---
## 🛠️ Ingress Controller

- Ingress kaynakları çalışması için cluster’da mutlaka bir Ingress Controller olmalı.
- Popüler Ingress Controllerlar: **NGINX**, **Traefik**, **Istio**, **HAProxy**.

---
## 📄 Basit Ingress YAML Örneği

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              number: 80
      - path: /app2
        pathType: Prefix
        backend:
          service:
            name: app2-service
            port:
              number: 80
```
## 🔍 Açıklamalar

| Alan              | Anlamı                                           |
| ----------------- | ------------------------------------------------ |
| `host`            | Trafiğin yönlendirileceği domain adı             |
| `path`            | URL yolu bazında yönlendirme (prefix veya exact) |
| `backend.service` | Hangi servis çağrılacak                          |
| Annotations       | Ingress controller’a özel ek ayarlar             |
## 🔧 Ingress Controller Kurulumu

- Örnek: NGINX Ingress Controller kurulumu
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.7.0/deploy/static/provider/cloud/deploy.yaml
```
## 🛡️ TLS ile HTTPS
Ingress TLS tanımı:
```yaml
spec:
  tls:
  - hosts:
    - example.com
    secretName: tls-secret
```
*TLS sertifikası `secretName` ile belirtilir*
## 💡 İpuçları

- Ingress, dış dünyaya servis expose etmek için en yaygın yöntem.
- Ingress controller olmadan Ingress kaynakları çalışmaz.
- Prod ortamda mutlaka TLS kullan.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/services-networking/ingress/
- https://kubernetes.github.io/ingress-nginx/