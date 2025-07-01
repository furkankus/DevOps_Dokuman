# 🔐 Docker Güvenliği

## 🧠 Amaç

Container'ların izole ve güvenli çalışmasını sağlamak. Kötü amaçlı imajlardan, aşırı yetkiden ve dış tehditlerden korunmak.

---

## ⚠️ Temel Güvenlik Prensipleri

| Konu                     | Açıklama |
|--------------------------|----------|
| Least Privilege          | Container’lara minimum yetki verilmeli |
| Official Image Kullanımı | Docker Hub’daki resmi/verified imajlar tercih edilmeli |
| Read-Only File System    | Mümkünse container sadece okuma izniyle çalışmalı |
| Root Olarak Çalıştırma   | Root ile çalışan imajlar tehlikelidir |
| Secrets Yönetimi         | Şifre, token gibi bilgiler çevre değişkeni yerine secret manager ile saklanmalı |

---

## 🛠️ Güvenlik Odaklı Komutlar

### 🔹 Container’ı Root Olmadan Çalıştırmak

```dockerfile
# Dockerfile içinde
RUN adduser -D appuser
USER appuser
```

```bash
docker run --user 1001 myimage
```
# 🔹 Dosya Sistemini Sadece Okunur Yapmak
```bash
docker run --read-only nginx
```
# 🔹 Ağ Erişimini Sınırlamak
```bash
docker network create --internal isolated_net
docker run --network=isolated_net app
```

***--internal` ağ ile dış dünyaya çıkılamaz.

# 🧰 Güvenlik Araçları
### 📦 `docker scan` (Snyk ile entegre)
```bash
docker scan nginx
```
***Resmi imaj üzerinde bilinen açıklar varsa rapor verir.***
# 🧪 `dockle` (image linter)
```bash
dockle myimage
```
***Dockerfile içindeki kötü uygulamaları (örneğin: root user, açık port) raporlar.

# 🔍 `trivy` (image vulnerability scanner)
```bash
trivy image node:18
```
***Yazılım paketlerindeki zafiyetleri listeler.

# 🛡️ Compose Dosyasında Güvenlik

```yaml
services:
  app:
    image: node
    user: "1001:1001"
    read_only: true
    cap_drop:
      - ALL
    security_opt:
      - no-new-privileges:true
```
***Ekstra yetkileri iptal eder, izinsiz yükseltmeyi engeller.

## ✅ Docker'da Güvenlik Checklist

- [ ]  Sadece gerekli portları aç
- [ ]  Official/verified imajlar kullan
- [ ]  Gereksiz `apt install` satırlarını sil
- [ ]  Volume'larda hassas verileri dışarı sızdırma
- [ ]  `--cap-drop ALL` kullan, sonra tek tek ihtiyaç duyulanı `--cap-add` ile ekle
- [ ]  .env dosyalarını git repo'larına koyma

## 🔗 Kaynaklar / Linkler

- https://docs.docker.com/security/
- [https://github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy)
- [https://github.com/goodwithtech/dockle](https://github.com/goodwithtech/dockle)
- https://snyk.io/docs/docker/