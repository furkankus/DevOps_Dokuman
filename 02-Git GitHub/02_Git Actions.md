# 🤖 GitHub Actions ile CI/CD

## 🧠 Amaç

Kod deposuna yapılan her değişiklikte (push, pull request vb.) otomatik olarak test, build, deploy gibi işlemleri gerçekleştirebilen bir CI/CD sistemi kurmak.

---

## 🛠️ Komutlar ve Yapılar

### 🔹 Temel Yapı (workflow dosyası)

```markdown

# .github/workflows/main.yml

name: CI Süreci

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Repo'yu klonla
        uses: actions/checkout@v3

      - name: Node.js kurulumu
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Bağımlılıkları yükle
        run: npm install

      - name: Testleri çalıştır
        run: npm test
```
# 🔹 `on` Anahtarı – Tetikleme Olayları
```yaml
on:
  push:
  pull_request:
  workflow_dispatch:    # Manuel tetikleme
  schedule:             # Zamanlayıcı (cron)
    - cron: '0 3 * * *' # Her gün 03:00'te
```
# 🔹 `jobs` – Aşamalar (Build, Test, Deploy)

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy adımı
        run: echo "Deploy işlemi burada yapılır"
```
# 🔹 Faydalı Action'lar
| Amaç           | Kullanım                                     |
| -------------- | -------------------------------------------- |
| Checkout       | `uses: actions/checkout@v3`                  |
| Node Kurulumu  | `uses: actions/setup-node@v3`                |
| Docker Login   | `uses: docker/login-action@v3`               |
| Azure Deploy   | `uses: azure/webapps-deploy@v2`              |
| Slack Bildirim | `uses: slackapi/slack-github-action@v1.24.0` |
## 📦 Örnek

### 📘 Uygulama: Basit bir Node.js test süreci

1. `package.json` içinde test script’in varsa (`"test": "jest"` gibi):

```yaml
name: Node Test

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm test
```


---

## ❗️Dikkat Edilecek Noktalar

- Workflow dosyaları `.github/workflows/` içinde yer almalı
- `secrets` (API Key, şifre vb.) verileri GitHub GUI üzerinden girilmeli
- Her `job` birbirinden bağımsızdır (artifacts ile paylaşım yapılabilir)
- Her işlem `ubuntu-latest`, `windows-latest`, `macos-latest` gibi sanal makinelerde çalışır
---
## 🔗 Kaynaklar / Linkler

- [https://docs.github.com/actions](https://docs.github.com/actions) – Resmi dökümantasyon
- [https://github.com/marketplace/actions](https://github.com/marketplace/actions) – Hazır Action’lar
- https://actions-cool.github.io/github-action-branding/ – Aksiyonlar için logo oluşturucu