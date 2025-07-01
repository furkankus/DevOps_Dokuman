## 📄 Dosya: `Docker_Volume.md`


# 💾 Docker Volume (Veri Kalıcılığı)

## 🧠 Amaç

Container’ların yeniden başlatıldığında bile veri kaybetmemesi için kalıcı depolama çözümlerini öğrenmek.

---

## 🛠️ Komutlar

### 🔹 Volume Yönetimi
```bash
docker volume create db-veri           # Yeni volume oluştur
docker volume ls                       # Volume listesi
docker volume inspect db-veri          # Volume detaylarını göster
docker volume rm db-veri               # Volume sil
```
# 🔹 Volume ile Container Çalıştırmak
```bash
docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=1234 \
  -v db-veri:/var/lib/mysql \
  mysql:5.7

```
***`db-veri` volume’u, MySQL verilerini kalıcı tutar.***
# 📦 Volume vs Bind Mount

|Özellik|Volume|Bind Mount|
|---|---|---|
|Yönetim|Docker tarafından|Host işletim sistemiyle|
|Yol|`/var/lib/docker/volumes/...`|Belirli bir klasör (örn. `/home/furkan/app`)|
|Yedekleme kolaylığı|Daha kolay|Manuel işlem gerekebilir|
|Kullanım amacı|Kalıcı veriler (db, uploads)|Geliştirme (kod klasörü paylaşımı)|
# 📘 Bind Mount Örneği
```bash
docker run -v $(pwd)/html:/usr/share/nginx/html nginx
```
# 📘 Volume ile Docker Compose
```bash
services:
  db:
    image: mysql
    volumes:
      - db-data:/var/lib/mysql

volumes:
  db-data:
```
## ❗️Dikkat Edilecek Noktalar

- Volume silinse bile container durmadan veri gitmez (ancak restart sonrası veri kaybı olur).
- Volume’lar Docker tarafından yönetilir ve sistem klasöründe tutulur.
- Volume yerine bind mount kullanırken dikkat: Linux/Windows yol farkları önemlidir.
---

## 🔗 Kaynaklar / Linkler

- https://docs.docker.com/storage/volumes/
- https://dockerlabs.collabnix.com/volume/
- https://docs.docker.com/storage/bind-mounts/