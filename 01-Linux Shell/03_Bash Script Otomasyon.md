# 🛠️ Bash Script ile Otomasyon

## 🧠 Amaç

Tekrarlanan işlemleri otomatikleştirmek, manuel komutları script hâline getirerek zaman kazandırmak ve hata riskini azaltmak.

---
Her bash script dosyasının başında olmalı. `bash` kabuğunu kullanacağını belirtir.

# 🔹 Değişken Tanımı
```bash
isim="Furkan"
echo "Merhaba $isim"

```
# 🔹 Koşullu İfadeler
```bash
if [ "$sayi" -gt 10 ]; then
  echo "Sayı 10'dan büyük"
else
  echo "Sayı 10 veya daha küçük"
fi
```
# 🔹 Döngüler
```bash
for i in {1..5}; do
  echo "Adım $i"
done

while true; do
  echo "Sonsuz döngü"
  break
done
```
# 🔹 Fonksiyonlar
```bash
selamla () {
  echo "Merhaba $1"
}

selamla Furkan
```
## 📦 Örnek

### 📘 Uygulama: Belirli bir klasördeki `.log` dosyalarını `.bak` olarak yedekle

```bash
`#!/bin/bash for file in /var/log/*.log; do   cp "$file" "$file.bak" done`
```

---

## ❗️Dikkat Edilecek Noktalar

Script çalıştırılmadan önce çalıştırma izni verilmeli:

`chmod +x script.sh`

Değişkenlerin başına `$` koyarak çağırmayı unutma

`exit` ile scriptin çalışmasını durdurabilirsin (örneğin hata varsa)


---

## 🔗 Kaynaklar / Linkler

- https://linuxconfig.org/bash-scripting-tutorial
    
- [https://www.shellscript.sh](https://www.shellscript.sh)
    
- [https://explainshell.com](https://explainshell.com)