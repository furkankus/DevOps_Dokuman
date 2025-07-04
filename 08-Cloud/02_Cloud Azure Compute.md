# 🖥️ Azure Cloud – Compute (Hesaplama) Servisleri

## 🧠 Amaç

Azure üzerinde uygulama çalıştırmak için kullanılan farklı compute servislerini, kullanım senaryolarıyla öğrenmek.

---
## 🧱 Compute Nedir?

"Compute", uygulamaların çalıştığı altyapı bileşenleridir. Bu; bir sunucu, bir konteyner veya sunucusuz bir işlem olabilir.

---
## 🔩 1. Azure Virtual Machines (VM)

### ✅ Açıklama:
- Azure’un IaaS çözümüdür.
- Windows veya Linux tabanlı sunucular oluşturabilirsin.

### 📦 Özellikler:
- Tam kontrol: RAM, CPU, disk vs.
- SSH/RDP ile erişim
- Snapshot, scale set, availability zone desteği

```bash
az vm create \
  --resource-group myRG \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```
---
## 🌐 2. Azure App Service

### ✅ Açıklama:

- Web uygulamaları ve API’ler için **PaaS** platformu
- Docker image ile de kullanılabilir (Web App for Containers)

### 📦 Özellikler:

- Otomatik ölçeklenebilir
- GitHub / DevOps CI/CD entegrasyonu
- SSL, slot, custom domain destekler

---
## 🔁 3. Azure Functions

### ✅ Açıklama:

- Sunucusuz (Serverless) uygulama mantığı
- Sadece işlem süresi kadar ücret ödenir

### 📦 Özellikler:

- Event-driven çalışır (HTTP, Queue, Timer)
- .NET, Node.js, Python, Java desteği
- Durable Functions ile background işlemler

---
## 🧱 4. Azure Kubernetes Service (AKS)

### ✅ Açıklama:

- Azure üzerinde tam yönetilen Kubernetes servisi
- Kendi container orkestrasyonunu sağlamak için kullanılır

### 📦 Özellikler:

- Node scaling
- Azure CLI ile kolay kurulum
- CI/CD entegrasyonu ve Helm desteği
```bash
az aks create \
  --resource-group myRG \
  --name myAKS \
  --node-count 2 \
  --enable-addons monitoring \
  --generate-ssh-keys
```
---
## 🚀 5. Azure Container Instances (ACI)

### ✅ Açıklama:

- Kubernetes veya VM kullanmadan hızlıca konteyner çalıştırmak için ideal
- Geçici işler, cronjob’lar için uygundur
```bash
az container create \
  --resource-group myRG \
  --name myContainer \
  --image nginx \
  --dns-name-label mycontainer123 \
  --ports 80
```
---
## 📊 Karşılaştırma Tablosu

|Servis|Model|Kullanım Durumu|
|---|---|---|
|VM|IaaS|Maksimum kontrol, özel yapı|
|App Service|PaaS|Web app, hızlı deploy|
|Azure Functions|Serverless|Event bazlı işlemler|
|AKS|CaaS|Mikroservis mimarisi|
|Container Instances|Serverless|Hızlı konteyner çalıştırma|

---
## 💡 En İyi Kullanım Senaryoları

- Web API için: **App Service**
- Mikroservis: **AKS**
- Anlık görevler: **Functions / ACI**
- Gelişmiş kurulum ve özelleştirme: **VM**

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/virtual-machines/](https://learn.microsoft.com/en-us/azure/virtual-machines/)
- [https://learn.microsoft.com/en-us/azure/app-service/](https://learn.microsoft.com/en-us/azure/app-service/)
- [https://learn.microsoft.com/en-us/azure/azure-functions/](https://learn.microsoft.com/en-us/azure/azure-functions/)
- [https://learn.microsoft.com/en-us/azure/aks/](https://learn.microsoft.com/en-us/azure/aks/)
- [https://learn.microsoft.com/en-us/azure/container-instances/](https://learn.microsoft.com/en-us/azure/container-instances/)