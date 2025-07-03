# ☁️ Azure Cloud – Giriş

## 🧠 Amaç

Bulut bilişimi, servis modellerini (IaaS, PaaS, SaaS) ve Microsoft Azure altyapısını genel hatlarıyla öğrenmek.

---
## 🌐 Cloud (Bulut) Nedir?

Cloud, internet üzerinden erişilebilen sunucu, veri tabanı, depolama, ağ ve yazılım kaynaklarının dinamik olarak sağlandığı platformdur.

---
## 🏷️ Servis Modelleri

| Model | Açıklama | Örnek |
|-------|----------|-------|
| **IaaS** | Infrastructure as a Service: Sanal makineler, disk, network gibi donanım katmanını içerir | Azure VM, Azure VNet |
| **PaaS** | Platform as a Service: Uygulama çalıştırma platformu sağlar, donanımı yönetmek gerekmez | Azure App Service, Azure SQL |
| **SaaS** | Software as a Service: Tamamen hazır uygulamalar | Office 365, Gmail, Dropbox |

---
## 🧱 Azure Nedir?

- Microsoft’un bulut platformudur.
- Yüzlerce servis sunar: VM, App Service, Kubernetes (AKS), Functions, Storage, Logic Apps, vs.
- Global veri merkezleriyle yüksek erişilebilirlik sağlar.

---
## 🗺️ Azure Temel Kavramlar

| Kavram         | Açıklama |
|----------------|----------|
| **Subscription** | Faturalama ve kaynak yönetiminin temelidir |
| **Resource Group** | Kaynakları mantıksal olarak gruplamak için kullanılır |
| **Region** | Fiziksel veri merkezi (örnek: West Europe) |
| **Availability Zone** | Aynı region içinde ayrı fiziksel konumlar |
| **Resource** | Azure'daki hizmetlerin her biri (VM, Storage, DB...) |

---
## 🧰 Azure Portal ve Azure CLI

| Araç         | Açıklama |
|--------------|----------|
| **Azure Portal** | Web arayüzüdür, kaynakları görsel olarak yönetmeyi sağlar |
| **Azure CLI**    | Komut satırı üzerinden yönetim imkanı verir |
| **Azure PowerShell** | PowerShell ile Azure yönetimi yapılabilir |

```bash
az login
az group create --name myRG --location westeurope
az vm create --resource-group myRG --name myVM --image UbuntuLTS
```
---
## 🧩 Azure'da Sık Kullanılan Servisler

|Servis|Açıklama|
|---|---|
|**Azure VM**|Sanal makine|
|**Azure App Service**|Web uygulaması barındırma platformu|
|**Azure AKS**|Azure Kubernetes Service|
|**Azure Blob Storage**|Dosya, medya, yedek saklamak için obje depolama|
|**Azure SQL**|Yönetilen veritabanı servisi|
|**Azure Key Vault**|Gizli bilgiler ve sertifika yönetimi|

---
## 🎯 Neden Azure?

✅ Microsoft ekosistemine tam entegrasyon  
✅ Hybrid cloud ve on-prem uyumu  
✅ Kurumsal destek ve SLA  
✅ Active Directory, DevOps, VS Code gibi araçlarla entegre çalışma

---
## 🔐 Güvenlik ve Erişim

- Azure AD ile kimlik yönetimi
- Role-Based Access Control (RBAC)
- Network Security Group (NSG), Firewall, Private Link gibi servislerle erişim kontrolü

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/](https://learn.microsoft.com/en-us/azure/)
- [https://azure.microsoft.com/en-us/get-started/](https://azure.microsoft.com/en-us/get-started/)
- [https://learn.microsoft.com/en-us/training/paths/azure-fundamentals/](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals/)