# 🔐 Kubernetes Güvenliği – Prensipler ve En İyi Uygulamalar

## 🧠 Amaç

Kubernetes ortamını ve uygulamalarını güvenli hale getirmek için temel güvenlik önlemlerini öğrenmek.

---
## 🔍 Temel Güvenlik Konuları

- **RBAC**: Yetkilendirme kontrolü
- **Network Policies**: Podlar arası trafik kontrolü
- **Pod Security Policies** (PSP) / Pod Security Standards: Pod güvenlik kısıtlamaları
- **Image Güvenliği**: Güvenilir container imajları kullanımı
- **Secret Yönetimi**: Hassas verilerin güvenli saklanması
- **Audit Logları**: Güvenlik olaylarının takibi

---
## 🔧 Network Policy Örneği
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
  namespace: default
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```
## 🔑 RBAC ile Yetkilendirme

- Daha önce detaylı öğrendiğin RBAC, erişimlerin kontrolünde kritik.
---
## 🔒 Secret Yönetimi

- Secrets base64 ile encode edilir, şifrelenmez.
- Daha güvenli saklama için Vault gibi çözümler tercih edilir.
---
## 🛡️ Pod Security Standards

- Podların yetki sınırlandırmaları ve güvenlik kuralları.
- Privileged container kullanımını minimize et.
---
## 🧹 İmaj Güvenliği

- Güvenilir registry kullan.
- Güncel ve az katmanlı (lightweight) imaj tercih et.

---
## 💡 İpuçları

- NetworkPolicy ile trafiği kısıtla.
- Pod güvenlik ayarlarını katı tut.
- RBAC izinlerini en az yetki prensibine göre ver.
- Düzenli güvenlik taramaları yap.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/security/overview/
- https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
- https://kubernetes.io/docs/concepts/services-networking/network-policies/