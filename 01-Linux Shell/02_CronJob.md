# ⏰ CronJob ile Otomatik Yedekleme

## 🧠 Amaç

Belirli zamanlarda otomatik olarak çalışan görevler tanımlayarak yedekleme, log temizleme, sistem kontrolü gibi işleri otomatikleştirmek.

---
## 🛠️ Komutlar

### 🔹 Cron zamanlama formatı:

```bash
| | | | |
| | | | +----- Haftanın günü (0-6) Pazar=0
| | | +------- Ay (1-12)
| | +--------- Gün (1-31)
| +----------- Saat (0-23)
+------------- Dakika (0-59)
```
# 🔹 Crontab komutları
```bash
crontab -e          # Cron görevlerini düzenle 
crontab -l          # Kayıtlı görevleri listele 
crontab -r          # Tüm cron görevlerini sil`
```
## 📦 Örnek

### 📘 Uygulama: Her gece 02:00'de bir klasörü yedekle

1. `backup.sh` dosyasını oluştur:

```bash
#!/bin/bash tar -czf /home/kullanici/backup_$(date +\%F).tar.gz /home/kullanici/veriler
```

2. Cron’a ekle:
   
```bash
0 2 * * * /home/kullanici/backup.sh
```

> Bu satır `crontab -e` ile dosyaya yazılır.

---

## ❗️Dikkat Edilecek Noktalar

- Cron ortamı, normal shell’den farklıdır → `PATH`, `ENV` değişkenlerini belirt
    
- Scriptin mutlak yolunu kullan
    
- Script çalıştırma izni olmalı:

```bash
   chmod +x backup.sh
```
---
## 🔗 Kaynaklar / Linkler

- [https://crontab.guru](https://crontab.guru) – Cron zamanlarını anlamak için süper
- `man 5 crontab` – Terminalden cron syntax açıklamaları
- https://opensource.com/article/19/7/cron-linux