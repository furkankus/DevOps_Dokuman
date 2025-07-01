# 🌐 Kubernetes Networking – Ağ Mimarisi ve İletişim

## 🧠 Amaç

Kubernetes içindeki podlar, servisler ve node’lar arasındaki ağ iletişimini anlamak ve CNI (Container Network Interface) eklentilerinin rolünü öğrenmek.

---
## 🧩 Temel Kavramlar

| Terim          | Açıklama |
|----------------|----------|
| **Pod Network** | Podların birbirleriyle iletişim kurduğu ağ. Her pod kendi IP adresine sahiptir. |
| **Service Network** | Servislerin IP adreslerinin bulunduğu ağ. Podlara erişimde kullanılır. |
| **Node Network** | Fiziksel veya sanal sunucuların (node’ların) bağlı olduğu ağ. |
| **CNI**         | Kubernetes’in ağ yapılandırmasını yöneten eklenti standartı (Calico, Flannel, Weave, vs.) |

---

## 🔗 Pod-to-Pod İletişim

- Tüm podlar cluster içindeki diğer podlara IP ile erişebilir.
- Kubernetes, her pod’a benzersiz bir IP verir.
- Pod IP’leri genellikle 10.x.x.x veya 192.168.x.x gibi özel ağ aralıklarından olur.

---
## 🌉 Service ve Ağ Erişimi

- Servisler, pod’ların sabit IP ya da DNS ile erişilmesini sağlar.
- Service ClusterIP ile pod IP’lerinden bağımsız sabit erişim noktası oluşturur.

---
## 🛠️ CNI (Container Network Interface) Eklentileri

| Eklenti  | Açıklama |
|----------|----------|
| **Calico** | Güçlü ağ politikaları ve güvenlik sağlar |
| **Flannel** | Basit ve hızlı kurulum için popüler |
| **Weave** | Çoklu cluster ağ kurulumlarında kullanılır |

---
## 📌 Network Policy

- Podlar arasındaki trafik kısıtlanabilir.
- Güvenlik amaçlı hangi podların hangi podlara erişebileceği belirlenir.

---
## 🔧 Ağ CIDR Örnekleri

- Pod Network CIDR: `10.244.0.0/16`
- Service Network CIDR: `10.96.0.0/12`

 *Bu IP blokları cluster kurulurken belirlenir.*

---
## 🔍 Ağ Sorunları ve Çözüm

- Podlar arası ping olmaması → CNI eklentisi kurulumu veya konfigürasyonu kontrol edilmeli.
- Service IP erişilemiyorsa → Service tanımı ve selector kontrol edilmeli.

---
## 🔗 Kaynaklar

- [https://kubernetes.io/docs/concepts/cluster-administration/networking/](https://kubernetes.io/docs/concepts/cluster-administration/networking/)
- [https://www.cni.dev/](https://www.cni.dev/)
- [https://docs.projectcalico.org/](https://docs.projectcalico.org/)
