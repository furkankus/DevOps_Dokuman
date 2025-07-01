## 🧠 Amaç

Birden fazla container içeren uygulamaları tek bir YAML dosyasıyla tanımlamak ve kolayca başlatmak, durdurmak, konfigüre etmek.

---

## 📜 Temel Yapı – `docker-compose.yml`

```yaml
version: '3.9'

services:
  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: appdb
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```
# 🛠️ Kullanılan Anahtarlar
| Alan          | Açıklama                                         |
| ------------- | ------------------------------------------------ |
| `version`     | Compose dosyası versiyonu                        |
| `services`    | Her bir container için yapılandırma alanı        |
| `image`       | Kullanılacak image (Docker Hub’dan ya da local)  |
| `build`       | Dockerfile ile image oluşturmak için kullanılır  |
| `ports`       | Port yönlendirmesi (host:container)              |
| `volumes`     | Kalıcı veri tutmak için kullanılır               |
| `environment` | Ortam değişkenleri (örn: şifre, config)          |
| `depends_on`  | Başlama sıralamasını belirtir (sadece sıra için) |
# 🚀 Komutlar
```bash
docker compose up            # Compose dosyasındaki tüm container'ları çalıştır
docker compose up -d         # Arka planda çalıştır
docker compose down          # Tüm container'ları durdur ve sil
docker compose build         # Dockerfile ile image oluştur
docker compose ps            # Çalışan container listesi
docker compose logs          # Logları göster
docker compose exec web bash # Belirli container’a gir
```
***Not: Bazı sistemlerde `docker-compose` yerine `docker compose` yazılmalı (yeni sürümde birleşti).

# 📦 Uygulama Örneği: Node.js + MongoDB
### 📁 Proje Yapısı
```bash
myapp/
├── docker-compose.yml
├── backend/
│   └── Dockerfile
└── ...
```
# 🐳 `docker-compose.yml`
```yaml
version: '3.9'

services:
  app:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```
## ❗️Dikkat Edilecek Noktalar

- `depends_on` sadece **başlangıç sırasını** garanti eder; servis hazır mı, onu kontrol etmez
- `volumes` sayesinde container silinse bile veriler silinmez
- `build` ile kendi Dockerfile’ını kullanabilirsin (örn: `build: ./app`)
- Ortam değişkenlerini ayrı `.env` dosyası ile tanımlayabilirsin
---

## 🔗 Kaynaklar / Linkler

- https://docs.docker.com/compose/
- https://dev.to/docker/ – Güncel Compose örnekleri
- [https://github.com/docker/awesome-compose](https://github.com/docker/awesome-compose) – Örnek projeler