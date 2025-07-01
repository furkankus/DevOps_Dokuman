## 🧠 Amaç

Docker ile container yönetimi, imaj işlemleri, volume kullanımı gibi temel ve ileri düzey komutları öğrenmek.

---

## 🛠️ Temel Komutlar

### 🔹 Docker Versiyon ve Bilgi
```bash
docker version      # Versiyon bilgisi
docker info         # Genel sistem durumu
```
# 📦 Image Komutları
## 🔹 İmaj Yönetimi
```bash
docker pull nginx                # Docker Hub'dan image indir
docker images                    # Tüm image'ları listele
docker rmi nginx                 # İmaj sil
docker build -t benim-imajim .   # Dockerfile'dan imaj oluştur
```
# 🚀 Container Komutları
## 🔹 Container Oluştur / Çalıştır
```bash
docker run hello-world                    # Test imajı çalıştır
docker run -d -p 8080:80 --name web nginx # Arka planda nginx
docker run -it ubuntu bash                # Etkileşimli terminal ile çalıştır
```
## 🔹 Container Yönetimi
```bash
docker ps                          # Çalışan container'ları listele
docker ps -a                       # Tüm container'ları (duranlar dahil)
docker stop <id|isim>             # Container'ı durdur
docker start <id|isim>            # Durdurulmuş container'ı başlat
docker restart <id|isim>          # Yeniden başlat
docker rm <id|isim>               # Container'ı sil
```
# 🧹 Sistem Temizleme Komutları
```bash
docker system prune               # Kullanılmayan her şeyi sil (tehlikeli)
docker image prune                # Boşta duran image’ları temizle
docker container prune            # Durdurulmuş container’ları sil
```
# 🔍 İnceleme ve Debug
```bash
docker logs <id|isim>             # Logları göster
docker exec -it <id> bash         # Çalışan container içine gir
docker inspect <id|isim>          # JSON formatında detaylı bilgi
docker top <id>                   # Container içindeki işlemler
```
# 📁 Volume ve Bind Mount
```bash
docker volume create yedeklerim             # Volume oluştur
docker volume ls                            # Volume listesi
docker run -v yedeklerim:/veri ubuntu       # Volume mount et
docker run -v $(pwd):/app nginx             # Bind mount ile dosya paylaş
```
# 🧪 Network Komutları
```bash
docker network ls                   # Ağları listele
docker network create web-agim      # Yeni ağ oluştur
docker network inspect bridge       # Ağ detaylarını görüntüle
docker network connect mynet cont1  # Container'ı ağa bağla
```
# 📘 Uygulama Örneği
```bash
# Yeni bir image build et ve çalıştır
docker build -t basit-api .
docker run -d -p 5000:5000 basit-api
```
## ❗️Dikkat Edilecek Noktalar

- `docker run` her çağrıldığında yeni bir container oluşturur
- `docker exec` sadece çalışan container’a girer
- `docker logs` sadece stdout/stderr çıktısını verir
- `docker system prune` geri alınamaz, dikkatli kullanılmalı!
---
## 🔗 Kaynaklar / Linkler

- https://docs.docker.com/engine/reference/commandline/docker/
- https://cheat.sh/docker – Hızlı komut rehberi
- https://dockerlabs.collabnix.com – Pratik Docker örnekleri