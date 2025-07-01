# 🌐 GitFlow Branch Stratejisi

## 🧠 Amaç

Projelerde dallanma (branching) modelini anlamak, geliştirme ve yayın süreçlerini düzenli bir yapıda yönetmek.

---
## 🛠️ Komutlar

### 🔹 Ana Branch'ler

- `main` → Yayında olan, kararlı kod
- `develop` → Aktif geliştirme yapılan dal

### 🔹 Yardımcı Branch'ler

- `feature/` → Yeni özellik geliştirmeleri
- `hotfix/` → Canlı sistemdeki acil düzeltmeler
- `release/` → Yayın öncesi test ve düzeltmeler

---
### 🔹 Komut Örnekleri
```bash
git checkout -b develop main                   # develop dalını main'den türet
git checkout -b feature/arama-sistemi develop  # yeni özellik dalı aç
git checkout -b release/v1.0 develop           # yayın dalı aç
git checkout -b hotfix/login-bug main          # canlıya acil düzeltme
```
## 📦 Örnek

### 📘 Uygulama: Feature branch ile geliştirme


```bash
git checkout -b feature/blog-ekleme develop # Kodları geliştir 
git add . 
git commit -m "Blog özelliği eklendi" 
git checkout develop 
git merge feature/blog-ekleme
```
---
## ❗️Dikkat Edilecek Noktalar

- Her branch belirli bir iş amacı için açılmalı (özellik, düzeltme vs.)
- Merge yaparken `develop` ve `main`'in güncel olduğuna emin olun
- Merge sonrası branch silinerek temizlik yapılmalı:
```bash
  git branch -d feature/blog-ekleme
```
---

## 🔗 Kaynaklar / Linkler

- https://nvie.com/posts/a-successful-git-branching-model/
- https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
- [https://git-scm.com/book/tr/v2](https://git-scm.com/book/tr/v2) – Türkçe Git kitabı