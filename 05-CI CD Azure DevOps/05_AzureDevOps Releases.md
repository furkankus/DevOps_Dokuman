# 🚀 Azure DevOps Releases – Dağıtım Süreci (CD)

## 🧠 Amaç

Azure DevOps üzerinde release pipeline’ı oluşturarak build edilen uygulamaların hedef ortamlara (örneğin test, staging, production) otomatik olarak dağıtımını öğrenmek.

---
## 🔍 Release Pipeline Nedir?

- Build sonucu üretilen artifact’ın farklı ortamlara dağıtılması işlemidir.
- Continuous Delivery / Deployment (CD) sürecinin bir parçasıdır.
- UI üzerinden (klasik şekilde) veya YAML ile yapılabilir (YAML genelde CI içindedir).

---
## 🧱 Release Pipeline Yapısı

| Bileşen        | Açıklama |
|----------------|----------|
| **Artifact**   | Build sonucu çıkan dosya |
| **Stages**     | Deployment aşamaları (örn: Test, QA, Prod) |
| **Tasks**      | Her aşamadaki adımlar (örn: Dosya kopyalama, servis restart) |
| **Approvals**  | Ortam geçişlerinde onay mekanizması |
| **Triggers**   | Release pipeline'ı ne zaman başlasın? (örn: her build sonrası)

---
## 🛠️ UI Üzerinden Release Pipeline Oluşturma

1. Azure DevOps > Pipelines > Releases
2. "New pipeline" > Artifact kaynağı olarak `Build` seç
3. Aşamalar (stage) ekle: `Staging`, `Production` gibi
4. Deployment adımlarını belirle:
   - Azure Web App deploy
   - IIS deploy
   - Kubernetes deployment
   - Shell script çalıştır
5. Gerekirse "Pre-deployment approval" ekle

---
## ⚙️ Yaygın Kullanılan Görevler (Tasks)

| Task                     | Amaç                              |
|--------------------------|-----------------------------------|
| **Azure App Service Deploy** | Azure Web App üzerine yayın |
| **Copy Files**           | Hedef makinaya dosya kopyalama     |
| **Publish Artifact**     | Build dosyalarını release’e alma   |
| **Azure CLI / SSH**      | Uzak makinada script çalıştırma    |

---
## 🔒 Onay Mekanizmaları (Approvals)

- Her stage’e özel onaycı atanabilir.
- Onay gelmeden sonraki aşamaya geçilmez.
- Manuel müdahale noktaları da eklenebilir (örneğin: `Manual Intervention` task'ı).

---
## 🔁 Trigger Türleri

- **After release creation:** Build sonrası otomatik başlatma
- **Scheduled:** Belirli zamanlarda çalıştırma
- **Manual:** Kullanıcı tetiklemeli

---
## 💡 İpuçları

- Ortam geçişleri için farklı yapılandırmalar (config dosyaları) kullan.
- Stage’ler arası geçişlerde farklı kullanıcı gruplarına yetki verebilirsin.
- Deployment’ı Azure, Linux VM, Kubernetes gibi pek çok hedefe yapabilirsin.

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/release/](https://learn.microsoft.com/en-us/azure/devops/pipelines/release/)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/release/deploy-using-templates](https://learn.microsoft.com/en-us/azure/devops/pipelines/release/deploy-using-templates)
