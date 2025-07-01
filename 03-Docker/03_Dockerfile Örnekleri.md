## 🧠 Amaç

Dockerfile ile özel container imajları oluşturmayı öğrenmek. Uygulamaya özel ihtiyaçlara göre örnek Dockerfile şablonlarını anlamak.

---
## 🛠️ Komutlar ve Temel Yapılar

### 🔹 Temel Dockerfile Komutları

| Komut     | Açıklama                                              |
| --------- | ----------------------------------------------------- |
| `FROM`    | Taban imajı belirler (örn: alpine, node, ubuntu)      |
| `RUN`     | İmaj oluşturulurken terminalde komut çalıştırır       |
| `COPY`    | Yerel dosyayı imaj içine kopyalar                     |
| `ADD`     | `COPY` gibidir, ayrıca arşiv ve URL desteği de vardır |
| `CMD`     | Container çalıştığında çalışacak komutu tanımlar      |
| `EXPOSE`  | Container'ın dışa açacağı portu belirtir              |
| `WORKDIR` | Çalışma dizinini tanımlar                             |
| `ENV`     | Ortam değişkeni tanımlar                              |

---
## 📦 Örnekler

# 📘 1. Basit Node.js Uygulaması Dockerfile

```dockerfile
# Base image
FROM node:18-alpine

# Uygulama klasörü
WORKDIR /app

# Paket dosyalarını kopyala
COPY package*.json ./

# Bağımlılıkları yükle
RUN npm install

# Diğer dosyaları kopyala
COPY . .

# Port aç
EXPOSE 3000

# Başlat
CMD ["node", "index.js"]
```
# 📘 2. Python Flask Uygulaması

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```
# 📘 3. Static HTML ile Nginx Kullanımı

```dockerfile
FROM nginx:alpine
COPY ./html /usr/share/nginx/html
EXPOSE 80
```
`./html` klasöründeki index.html vs. doğrudan Nginx ile yayınlanır.

# 📘 4. Alpine Üzerinden Bash Script Container

```dockerfile
FROM alpine
COPY backup.sh /usr/local/bin/backup.sh
RUN chmod +x /usr/local/bin/backup.sh
CMD ["backup.sh"]
```
# 📘 5. Multi-Stage Build – Prod için Temiz Node.js

```dockerfile
# 1. Aşama: Build
FROM node:18 AS build

WORKDIR /app
COPY . .
RUN npm install && npm run build

# 2. Aşama: Prod
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
```
Gereksiz dosyaları dışarıda bırakır, küçük ve güvenli imaj üretir.
## ❗️Dikkat Edilecek Noktalar

- `COPY . .` komutu `.dockerignore` dosyasına dikkat ederek çalışır
- `CMD` sadece bir defa kullanılabilir, çoklu komut için bash script yaz
- Her Dockerfile içinde `FROM` mutlaka olmalı
- `RUN`, imaj boyutunu artırır; aşırı kullanımdan kaçınılmalı
---
## 🔗 Kaynaklar / Linkler

- https://docs.docker.com/engine/reference/builder/
- [https://github.com/docker-library](https://github.com/docker-library) – Resmi base imajlar
- https://hub.docker.com/_/node – Node.js Docker imajı