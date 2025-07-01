# 🕸️ Kubernetes Service Mesh – Mikroservis İletişim ve Yönetimi

## 🧠 Amaç

Mikroservisler arasında güvenli, gözlemlenebilir ve yönetilebilir iletişim sağlamak için Service Mesh’i öğrenmek.

---
## 🤔 Service Mesh Nedir?

- Mikroservisler arasındaki trafiği yönetmek için altyapı katmanı.
- Trafik yönlendirme, servis keşfi, yük dengeleme, güvenlik (mTLS), gözlemlenebilirlik sağlar.
- Sidecar proxy (Envoy gibi) tabanlı çalışır.

---
## 🛠️ Popüler Service Meshler

| Service Mesh       | Açıklama                             |
|--------------------|------------------------------------|
| **Istio**          | En yaygın ve özellikli Service Mesh |
| **Linkerd**        | Hafif ve basit kullanım              |
| **Consul Connect** | HashiCorp’un Service Mesh çözümü    |

---
## 🔧 Istio Temel Bileşenleri

- **Envoy Proxy:** Sidecar olarak pod’lara eklenir.
- **Pilot:** Trafik yönetimi için konfigürasyon sağlar.
- **Mixer:** Telemetri ve politika yönetimi yapar.
- **Citadel:** Güvenlik ve sertifika yönetimi sağlar.

---
## 📦 Basit Istio Kurulumu

```bash
istioctl install --set profile=demo -y
kubectl label namespace default istio-injection=enabled
```
## 🔍 Trafik Yönetimi

- VirtualService ve DestinationRule kaynakları ile detaylı yönlendirme yapılır.

---
## 💡 İpuçları

- Service Mesh kullanımı ek kaynak ve karmaşıklık getirir.
- Performans ve güvenlik için faydalıdır.
- İyi öğrenip küçük projelerde denemek önerilir.

---
## 🔗 Kaynaklar

- https://istio.io/latest/docs/
- [https://linkerd.io/](https://linkerd.io/)