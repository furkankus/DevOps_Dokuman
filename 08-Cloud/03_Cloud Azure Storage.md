# 💾 Azure Cloud – Storage Servisleri

## 🧠 Amaç

Azure üzerindeki veri depolama çözümlerini, senaryolarla birlikte öğrenmek: Blob, File Share, Table, Queue ve Disk.

---
## 📦 Azure Storage Nedir?

- Microsoft Azure’un sunduğu **düşük maliyetli, yüksek erişilebilirlikli** veri depolama servisidir.
- Hem yapılandırılmış (structured) hem de yapılandırılmamış (unstructured) verileri destekler.
- Tüm Storage tipleri aynı "Storage Account" altında barındırılabilir.

---
## 🗂️ Azure Storage Türleri

| Tür                | Açıklama |
|--------------------|----------|
| **Blob Storage**   | Büyük dosyalar (medya, log, yedek) için uygundur |
| **File Storage**   | SMB üzerinden paylaşımlı dosya sistemi |
| **Table Storage**  | NoSQL anahtar-değer yapısında veriler |
| **Queue Storage**  | Asenkron mesajlaşma kuyusu |
| **Disk Storage**   | Azure VM’ler için disk alanı sağlar (OS/Veri diski) |

---
## 🪣 1. Azure Blob Storage

### ✅ Kullanım:
- Resim, video, yedekleme, log dosyaları gibi büyük nesneler

### 📁 Katmanlar:
- Hot: Sık erişilen veriler
- Cool: Seyrek erişilen veriler
- Archive: Uzun süre saklanan, nadiren erişilen veriler

```bash
az storage account create \
  --name mystorage123 \
  --resource-group myRG \
  --location westeurope \
  --sku Standard_LRS

az storage container create \
  --account-name mystorage123 \
  --name mycontainer \
  --public-access blob
```
---
## 📂 2. Azure File Share

- Dosya sunucusu gibi çalışır (SMB desteği)
- Uygulamalar arasında ortak dosya erişimi sağlar
- Windows ve Linux sistemlerden bağlanabilir
```bash
az storage share create \
  --account-name mystorage123 \
  --name myshare
```
---
## 🔑 3. Table & Queue Storage

- Table: Basit NoSQL tablo yapısı (key-value)
- Queue: Uygulamalar arası mesajlaşma kuyusu
```bash
az storage queue create \
  --account-name mystorage123 \
  --name myqueue
```
---
## 💽 4. Disk Storage

- VM’lere OS ya da veri diski eklemek için kullanılır.
- Premium (SSD), Standard (HDD) seçenekleri vardır.
```bash
az disk create \
  --resource-group myRG \
  --name myDataDisk \
  --size-gb 128 \
  --sku Premium_LRS
```
---
## 🔐 Güvenlik

- Private Endpoint ile erişimi sınırla
- Azure AD veya SAS token ile kimlik doğrulama
- Geo-Redundant Storage (GRS) ile felaket durumlarına karşı koruma

---
## 🔁 Yedekleme ve Erişim

|Katman|Erişim Süresi|Maliyet|
|---|---|---|
|Hot|< 1 sn|Yüksek|
|Cool|Saniyeler|Orta|
|Archive|Saatler|Düşük|

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/storage/](https://learn.microsoft.com/en-us/azure/storage/)
- [https://learn.microsoft.com/en-us/azure/storage/blobs/](https://learn.microsoft.com/en-us/azure/storage/blobs/)
- [https://learn.microsoft.com/en-us/azure/storage/files/](https://learn.microsoft.com/en-us/azure/storage/files/)
- [https://learn.microsoft.com/en-us/azure/storage/queues/](https://learn.microsoft.com/en-us/azure/storage/queues/)