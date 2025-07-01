## 📄 Dosya: `Docker_BestPractices.md`

# 🧠 Docker Best Practices (En İyi Uygulamalar)

## 🧠 Amaç

Verimli, güvenli, taşınabilir ve hızlı çalışan Docker container’ları oluşturmak için profesyonel kullanım kurallarını öğrenmek.

---
## 🛠️ Dockerfile Yazımında En İyi Uygulamalar

- ✅ Küçük base image kullan (örn: `alpine`)
- ✅ Katmanları azaltmak için `RUN` komutlarını birleştir:
```dockerfile
RUN apt update && apt install -y curl && rm -rf /var/lib/apt/lists/*
```
- ✅ Gereksiz dosyaları `.dockerignore` ile hariç tut
- ✅ Uygulamayı non-root user ile çalıştır
- ✅ `COPY` yerine `ADD` sadece gerekli durumlarda kullan
## 🧰 Image ve Build

- ✅ `docker build --no-cache` ile ilk kez temiz build yap
- ✅ İmage’lara versiyon etiketi ver (`myapi:1.0.0` yerine `myapi:latest` kullanma)
- ✅ Multi-stage build kullanarak imaj boyutunu küçült:
```dockerfile
FROM node:18 as builder
...
FROM nginx
COPY --from=builder /app/dist /usr/share/nginx/html
```
## 🔄 Container Kullanımı

- ✅ `--rm` ile iş bitince silinmesi sağlanabilir:
```bash
docker run --rm hello-world
```
- ✅ `--read-only`, `--cap-drop` gibi güvenlik bayrakları kullanılmalı
- ✅ Uygulamalar için environment variables `.env` dosyasıyla yönetilmeli
## 📁 Volume ve Mount

- ✅ Volume’ları `docker volume` ile yönetin, bind mount’u sadece geliştirmede tercih et
- ✅ Gizli bilgileri environment yerine secrets manager ile yönet
- ✅ `.env` dosyasını git’e koyma – `.gitignore` içinde olmalı7
## 🔥 Performans

- ✅ Network modunda `host` sadece gerektiğinde kullan
- ✅ Uygulamalar farklı container’larda çalışmalı (örn: app + db)
- ✅ `docker-compose` ile ortamları otomatikleştir
## 🔍 İzleme ve Loglama

- ✅ `docker logs` ile anlık çıktı kontrolü yap
- ✅ `docker stats` ile performans izleme yap
- ✅ Gelişmiş loglama için fluentd, ELK gibi sistemlerle entegre et
## 🔗 Kaynaklar

- https://docs.docker.com/develop/dev-best-practices/
- [https://github.com/hexops/dockerfile-best-practices](https://github.com/hexops/dockerfile-best-practices)
- https://snyk.io/blog/10-docker-image-security-best-practices/