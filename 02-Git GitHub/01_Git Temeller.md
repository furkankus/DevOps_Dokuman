# 🌿 Git Temelleri

## 🧠 Amaç

Versiyon kontrol sistemi olan Git'in temel komutlarını öğrenerek kod geçmişini takip edebilmek, geri dönebilmek ve ekiplerle verimli çalışabilmek.

---

## 🛠️ Komutlar

### 🔹 Git Başlangıç

```bash
git init                   # Yeni bir Git deposu başlat
git clone <repo-url>      # Mevcut bir uzak repoyu klonla
```
# 🔹 Durum ve Değişiklikler

```bash
git status                # Değişiklik durumunu göster
git add dosya.txt         # Dosyayı sahneye (staging) al
git add .                 # Tüm değişiklikleri sahnele
git commit -m "mesaj"     # Commit (kaydet) yap
```
# 🔹 Geçmiş ve Log

```bash
git log                   # Commit geçmişini listele
git log --oneline         # Tek satırlık geçmiş
```
# 🔹 Geri Alma
```bash
git reset dosya.txt       # Sahneleme alanından çıkar
git checkout -- dosya.txt # Dosyayı eski haline getir
git revert <commit_id>    # Commit'i geri al (tersini yap)
```

## 📦 Örnek

### 📘 Uygulama: Basit bir Git projesi oluşturmak

```bash
mkdir ornek-proje cd ornek-proje git init echo "# Ornek Proje" > README.md git add README.md git commit -m "İlk commit"
```

---

## ❗️Dikkat Edilecek Noktalar

- `git add .` tüm dosyaları sahneye alır, dikkatli kullanılmalı
- `git reset --hard` tüm yerel değişiklikleri siler, dikkatli olunmalı
- `commit` sadece yerel kayıt yapar → GitHub'a göndermek için `push` gerekir
---

## 🔗 Kaynaklar / Linkler

- https://learngitbranching.js.org – İnteraktif Git anlatımı
- [https://git-scm.com/docs](https://git-scm.com/docs) – Resmi Git dökümanları
- https://www.atlassian.com/git/tutorials