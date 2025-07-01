# 🐧 Linux Shell – Temel Komutlar

## 🧠 Amaç

Linux terminalinde sık kullanılan temel komutları öğrenmek, dosya/dizin işlemleri ve sistem yönetimini komut satırı üzerinden etkili şekilde yapabilmek.

---
## 🛠️ Komutlar

### 🔹 Dizin İşlemleri

```bash
pwd             # Mevcut dizini göster
ls              # Dizin içeriğini listele
ls -la          # Gizli dosyalarla birlikte detaylı listeleme
cd /klasor/yolu # Dizin değiştirme
cd ~            # Ana dizine git
```
# 🔹 Dosya İşlemleri
```bash
touch dosya.txt       # Yeni boş dosya oluştur`
mkdir yeni_klasor     # Yeni klasör oluştur`
cp kaynak hedef       # Dosya veya klasörü kopyala`
mv kaynak hedef       # Dosya taşı / yeniden adlandır`
rm dosya.txt          # Dosya sil`
rm -rf klasor/        # Klasör ve içeriğini zorla sil`
```

# 🔹 Dosya Görüntüleme
```bash
cat dosya.txt         # Dosya içeriğini görüntüle
less dosya.txt        # Sayfa sayfa görüntüleme
head dosya.txt        # İlk 10 satırı göster
tail dosya.txt        # Son 10 satırı göster
tail -f log.txt       # Dosya sonunu canlı izle
```
# 🔹 Kullanıcı ve Yetkiler
```bash
whoami                # Mevcut kullanıcıyı göster
id                    # Kullanıcının UID ve grup bilgisi
chmod +x script.sh    # Dosyaya çalıştırma izni ver
chown user:user dosya # Sahipliği değiştir
```
# 🔹 Arama ve Filtreleme  
```bash
grep "aranan" dosya.txt        # Dosyada kelime ara
find . -name "*.sh"            # *.sh dosyalarını ara
history                        # Komut geçmişini listele
```
# 🔹 Ağ Komutları
```bash
ping google.com                # Ağ bağlantısını test et
curl https://example.com       # Web içeriğini çek
ifconfig / ip a                # IP adreslerini göster
```
## 📦 Örnek

### 📘 Uygulama: Basit bir log dosyasını izle

```bash
`tail -f /var/log/syslog`
```

Bu komutla sistem loglarını anlık takip edebilirsin. Özellikle hata ayıklamada kullanılır.

---

## ❗️Dikkat Edilecek Noktalar

- `rm -rf` komutu dikkatli kullanılmalı. Yanlış klasörde tüm sistemi silebilirsin.
    
- `sudo` ile yapılan işlemler sistem seviyesinde değişiklik yapar. Gerekmedikçe kullanma.
    
- Terminalde yazılan her komut sistemde bir iz bırakır (history üzerinden takip edilebilir).
    

---

## 🔗 Kaynaklar / Linkler

- [https://explainshell.com](https://explainshell.com) – Komutları tek tek açıklayan site
    
- [https://linuxcommand.org](https://linuxcommand.org) – Başlangıç için Linux komut eğitimi
    
- [cheat.sh](https://cheat.sh) – Anında komut rehberi: `curl cheat.sh/ls`