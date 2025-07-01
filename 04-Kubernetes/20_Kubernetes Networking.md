# 🌐 Kubernetes Networking – Ağ Yapısı ve Servisler

## 🧠 Amaç

Kubernetes cluster içi ve dışı iletişimin nasıl gerçekleştiğini ve ağ yapılandırmalarını öğrenmek.

---
## 🔍 Kubernetes Ağının Temel Özellikleri

- Pod’lar birbirleriyle doğrudan iletişim kurabilir.
- Her Pod’un kendine özel IP adresi vardır.
- Node’lar arasında pod IP’leri erişilebilir olmalıdır.
- Servisler (Services) ile pod’lara sabit IP veya DNS atanır.

---
## 🛠️ Temel Kavramlar

| Kavram          | Açıklama                              |
|-----------------|-------------------------------------|
| **Pod Network** | Pod’lar arası IP iletişimi            |
| **Service**    | Pod grubuna sabit IP ve DNS sağlar    |
| **Ingress**    | Dış dünyadan cluster içindeki servislere trafik yönlendirme |
| **Network Plugin (CNI)** | Ağ yapılandırmasını sağlayan eklentiler (Calico, Flannel, Weave) |

---
## 📦 Service Türleri

| Tür             | Açıklama                          |
|-----------------|---------------------------------|
| **ClusterIP**  | Sadece cluster içinden erişim      |
| **NodePort**   | Node’un IP’si ve belirli porttan erişim |
| **LoadBalancer** | Bulut sağlayıcısında yük dengeleme  |
| **ExternalName** | DNS alias atama                  |

---
## 🔧 Basit Service Örneği

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 9376
  type: ClusterIP
```
## 🌐 Ingress Örneği
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```
## 🔌 Yaygın CNI Pluginleri

- **Calico:** Güvenlik ve politika yönetimi ile popüler.
- **Flannel:** Basit ve hızlı kurulum.
- **Weave:** Kolay yönetim ve iyi entegrasyon.

---
## 💡 İpuçları

- CNI plugin kurulumu cluster’ın ilk aşamalarındandır.
- NetworkPolicy ile pod iletişimini kontrol et.
- Servis tiplerini ve Ingress kurallarını doğru seç.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/cluster-administration/networking/
- https://kubernetes.io/docs/concepts/services-networking/service/
- https://kubernetes.io/docs/concepts/services-networking/ingress/