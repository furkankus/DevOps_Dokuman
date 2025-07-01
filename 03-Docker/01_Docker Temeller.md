## 🧠 Amaç

Docker ile uygulamaları izole ortamda (container içinde) çalıştırmayı öğrenmek. Docker imajları, container’lar ve temel kavramlarla tanışmak.

---

## 🛠️ Komutlar

### 🔹 Genel Komutlar
```bash
docker version          # Docker sürüm bilgisi
docker info             # Sistem durumu
docker help             # Yardım dökümantasyonu
```
# 🔹 Image (İmaj) İşlemleri
```bash
docker pull nginx                   # Docker Hub'dan image indir
docker images                       # Yerel image'ları listele
docker rmi nginx                    # Image sil
docker build -t benim-imageim .     # Dockerfile'dan image oluştur
```
# 🔹 Container İşlemleri
```bash
docker run hello-world             # Basit container çalıştır
docker run -d -p 8080:80 nginx     # Arka planda nginx başlat
docker ps                          # Çalışan container'ları göster
docker ps -a                       # Tüm container'ları göster (duranlar dahil)
docker stop <id>                   # Container durdur
docker start <id>                  # Durdurulmuş container'ı başlat
docker rm <id>                     # Container sil
```
# 🔹 Volume ve Mount
```bash
docker run -v /host/path:/container/path nginx
```

## 📦 Örnek

### 📘 Uygulama: Nginx container'ı çalıştır

```bash
docker run -d --name websunucu -p 8080:80 nginx
```

> Tarayıcıdan `localhost:8080` adresine giderek Nginx sayfasını görebilirsin.

---

## ❗️Dikkat Edilecek Noktalar

- Container silmeden önce durdurulmalı (`stop`)
- Port yönlendirmesini unutursan tarayıcıda erişemezsin
- `--rm` parametresiyle container iş bitince otomatik silinir
- `docker system prune` ile sistem temizliği yapılır (çok dikkatli kullanılmalı)
---
## 🔗 Kaynaklar / Linkler

- https://hub.docker.com – Resmi imajlar
- https://docs.docker.com/engine/reference/commandline/docker/
- [https://play-with-docker.com](https://play-with-docker.com) – Tarayıcıda canlı deneme ortamı