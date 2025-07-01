# 🧯 Docker Troubleshooting (Hata Ayıklama)

## 🧠 Amaç

Docker kullanırken karşılaşılan yaygın sorunları tespit etmek ve çözüm yöntemlerini öğrenmek.

---

## 🐳 Yaygın Hatalar ve Çözümleri

### ❌ Port Çakışması
```bash
Error starting userland proxy: listen tcp 0.0.0.0:80: bind: address already in use
```
**✅ Çözüm:**
- Farklı port seç (`-p 8080:80`)
- Portun kullanımda olup olmadığını kontrol et:
```bash
lsof -i :80
```
### ❌ "Image not found" veya "manifest unknown"
```bash
docker run my-custom-image
```
**✅ Çözüm:**
- `docker build` ile local image varsa `-t` ile isim verilmeli
- Public image çekiliyorsa doğru yazım kontrol edilmeli:
```bash
docker pull node:18
```
### ❌ "Permission Denied" (Volume/Bind Mount)
```bash
mkdir: cannot create directory ... Permission denied
```
**✅ Çözüm:**
- Volume’a yazma izni olmayabilir
- Container’ı root olmadan çalıştırıyorsan klasör izinlerini kontrol et:
```bash
chmod -R 777 ./veri_klasoru
```
### ❌ Container Hemen Kapanıyor
```bash
docker run alpine
#Container kapanır
```
**✅ Çözüm:**
- Etkileşimli/aktif bir komut girilmeli:
```bash
docker run -it alpine sh
```
*`CMD` satırı kontrol edilmeli (uygulama background’da çalışıyorsa `tail -f /dev/null` gibi komutlarla aktif tutulabilir)*
### ❌ Cannot connect to Docker Daemon
```bash
Got permission denied while trying to connect to the Docker daemon socket
```
✅ Çözüm:
```bash
sudo usermod -aG docker $USER
newgrp docker
```
## 🔍 Hata İnceleme Komutları
```bash
docker ps -a                 # Container durumu
docker logs <id|isim>        # Loglara bak
docker inspect <id|isim>     # JSON detay
docker events                # Canlı olay akışı
docker network inspect ...   # Ağ sorunları
```
## 🔗 Kaynaklar

- https://docs.docker.com/config/containers/logging/
- [https://github.com/docker/for-linux/issues](https://github.com/docker/for-linux/issues)
