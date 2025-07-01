# ⛵ Kubernetes Helm – Paket Yönetimi ve Kolay Dağıtım

## 🧠 Amaç

Kubernetes üzerinde uygulamaları kolayca paketlemek, versiyonlamak ve yönetmek için Helm kullanımını öğrenmek.

---
## 🚢 Helm Nedir?

- Kubernetes için popüler bir paket yöneticisidir.
- Uygulama manifest dosyalarını “chart” olarak paketler.
- Tek komutla kurulum, güncelleme, rollback sağlar.
- Karmaşık uygulama dağıtımlarını kolaylaştırır.

---
## 🛠️ Helm Kurulumu

```bash
# Helm binary indir ve kur (örnek Linux için)
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```
## 🎯 Temel Kavramlar

| Kavram         | Açıklama                                   |
| -------------- | ------------------------------------------ |
| **Chart**      | Helm paket dosyası (manifest ve şablonlar) |
| **Release**    | Chart’ın cluster’a kurulmuş hali           |
| **Repository** | Chartların bulunduğu depo                  |
## 🚀 Basit Helm Chart Kurulumu
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install my-nginx bitnami/nginx
```
## 📄 Chart Yapısı
```bash
mychart/
  Chart.yaml          # Chart bilgileri
  values.yaml         # Varsayılan değerler
  templates/          # Kubernetes manifest şablonları
```
## 🔧 Değerlerin Özelleştirilmesi
```bash
helm install my-app ./mychart --set replicaCount=3,image.tag=1.16.0
```
*Ya da `values.yaml` dosyasını düzenleyerek.*
## 🔁 Güncelleme ve Rollback
```bash
helm upgrade my-nginx bitnami/nginx --set replicaCount=5
helm rollback my-nginx 1
```
## 🧹 Kaldırma
```bash
helm uninstall my-nginx
```
## 💡 İpuçları

- Helm, YAML karmaşasını azaltır.
- Karmaşık uygulamaları tek seferde kolayca deploy eder.
- Versiyonlama ve rollback imkanı sayesinde güvenlidir.

---
## 🔗 Kaynaklar

- https://helm.sh/docs/
- https://artifacthub.io/packages/search?kind=0
