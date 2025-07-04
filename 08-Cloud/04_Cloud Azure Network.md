# 🌐 Azure Cloud – Networking

## 🧠 Amaç

Azure üzerindeki ağ servislerini ve bileşenlerini tanımak; güvenli, ölçeklenebilir ve erişilebilir uygulama altyapıları oluşturmayı öğrenmek.

---
## 🧱 Temel Bileşenler

| Bileşen           | Açıklama |
|-------------------|----------|
| **Virtual Network (VNet)** | Azure’daki özel IP’li sanal ağ |
| **Subnet**        | VNet içindeki küçük ağ bölümleri |
| **NSG (Network Security Group)** | Gelen ve giden trafiği kontrol eden güvenlik kuralları |
| **Public IP**     | Azure dışına açık IP adresi |
| **Load Balancer** | Trafiği birden çok backend’e dağıtan yapı |
| **Application Gateway** | Layer 7 (HTTP) yük dengeleme |
| **VPN Gateway**   | Şirket ağı ile Azure arasında bağlantı sağlar |
| **Private Link**  | Azure servisine özel ağdan güvenli bağlantı sağlar |

---
## 📦 1. Virtual Network (VNet)

```bash
az network vnet create \
  --name myVNet \
  --resource-group myRG \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```
- VNet = Azure üzerindeki özel sanal ağ
- Subnet = VNet içindeki küçük IP aralığı

---
## 🔐 2. NSG – Network Security Group

- Gelen ve giden trafiğe kurallar tanımlar
- IP, port, protokol bazında kısıtlamalar yapılır
```bash
az network nsg create \
  --resource-group myRG \
  --name myNSG

az network nsg rule create \
  --resource-group myRG \
  --nsg-name myNSG \
  --name AllowHTTP \
  --priority 100 \
  --destination-port-ranges 80 \
  --access Allow \
  --protocol Tcp \
  --direction Inbound
```
---
## 🌍 3. Public IP Adresi

- Azure dışından erişim için gereklidir
```bash
az network public-ip create \
  --resource-group myRG \
  --name myPublicIP
```
---
## ⚖️ 4. Load Balancer (Layer 4)

- VM’ler veya container’lar arasında trafik dağıtır
- Dış erişim için Public, iç erişim için Internal olabilir
```bash
az network lb create \
  --resource-group myRG \
  --name myLB \
  --frontend-ip-name myFrontEnd \
  --backend-pool-name myBackEndPool \
  --public-ip-address myPublicIP
```
---
## 🧭 5. Application Gateway (Layer 7)

- HTTP tabanlı trafik için **Web Application Firewall (WAF)** destekli yük dengeleyici
- Hostname, URL path’e göre yönlendirme yapabilir

---
## 🔐 6. VPN Gateway ve Private Link

|Bileşen|Kullanım|
|---|---|
|**VPN Gateway**|Şirket içi ağ ile Azure’u IPsec VPN ile bağlar|
|**Private Link**|Azure servisine doğrudan özel IP ile bağlanma sağlar|

---
## 🧮 CIDR ve IP Planlama

- CIDR: `10.0.0.0/16` → 65.536 IP
- Subnet: `10.0.1.0/24` → 256 IP
- Her subnet için 5 IP rezerve edilir (ilk 4 + son 1)

---
## 🧪 Diagnostik ve Güvenlik

|Servis|Amaç|
|---|---|
|**NSG Flow Logs**|Ağ trafiğini izlemek|
|**Network Watcher**|Ağ tanılaması|
|**Firewall**|Gelişmiş ağ güvenlik duvarı|

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/virtual-network/](https://learn.microsoft.com/en-us/azure/virtual-network/)
- [https://learn.microsoft.com/en-us/azure/networking/](https://learn.microsoft.com/en-us/azure/networking/)
- [https://learn.microsoft.com/en-us/azure/network-watcher/](https://learn.microsoft.com/en-us/azure/network-watcher/)