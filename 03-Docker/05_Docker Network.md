# 🌐 Docker Ağ (Network) Yapısı

## 🧠 Amaç

Container’lar arasında iletişim kurmak, izole ağ ortamları oluşturmak ve dış dünyaya açılma kurallarını anlamak.

---

## 🛠️ Komutlar

### 🔹 Ağları Listele / Oluştur / Sil

```bash
docker network ls                       # Ağları listele
docker network create benim-agim        # Yeni bir bridge ağı oluştur
docker network inspect bridge           # Ağ detaylarını görüntüle
docker network rm benim-agim            # Ağı sil
```

# 🔹 Container’ı Ağa Bağlamak
```bash
docker run -d --name app1 --network benim-agim nginx
docker network connect benim-agim app2
```
## 📘 Ağ Türleri

| Ağ Tipi   | Açıklama                                                         |
| --------- | ---------------------------------------------------------------- |
| `bridge`  | Varsayılan. Container'lar aynı ağdaysa birbirine erişebilir.     |
| `host`    | Container, host ile aynı ağ arabirimini kullanır (Linux'a özgü). |
| `none`    | Ağsız, tamamen izole container.                                  |
| `overlay` | Swarm/Kubernetes ortamında çoklu host’ta ağ kurar.               |
# 📦 Örnek: 2 Container Arası Özel Ağ
```bash
docker network create benim-net

docker run -d --name web --network benim-net nginx
docker run -it --name client --network benim-net alpine sh

# alpine içinde:
apk add curl
curl http://web
```
***`web` container’ı, aynı ağda olduğu için ismiyle erişilebilir.***
## ❗️Dikkat Edilecek Noktalar

- Container’lar yalnızca aynı ağ üzerindeyse doğrudan isimleriyle birbirine ulaşabilir.
- `bridge` ağı Docker tarafından otomatik oluşturulur ama özelleştirilebilir.
- Çoklu host için `overlay` ağı kullanılır (Swarm veya Kubernetes gerekebilir).
---

## 🔗 Kaynaklar / Linkler

- https://docs.docker.com/network/
- https://dockerlabs.collabnix.com/network/