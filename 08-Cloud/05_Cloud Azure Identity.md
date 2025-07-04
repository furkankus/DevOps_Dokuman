# 🔐 Azure Cloud – Identity & Access Management (IAM)

## 🧠 Amaç

Azure üzerinde kullanıcı, uygulama ve kaynaklar arasındaki erişim ve yetkilendirme süreçlerini öğrenmek.

---
## 👥 1. Azure Active Directory (Azure AD)

Azure’daki kimlik yönetim sistemidir. Kullanıcıları, grupları, uygulamaları ve servisleri merkezi olarak yönetir.

### 📌 Özellikler:
- Kurumsal kullanıcı yönetimi
- Uygulama entegrasyonu (SSO)
- MFA, Conditional Access, B2B & B2C destekler

---
## 🧑‍💻 2. Kullanıcı & Grup Yönetimi

```bash
az ad user create \
  --display-name "Ahmet Yılmaz" \
  --user-principal-name ahmet@mydomain.onmicrosoft.com \
  --password MyPassword123!

az ad group create \
  --display-name DevOpsTeam \
  --mail-nickname devopsteam
```
---
## 🛂 3. Role-Based Access Control (RBAC)

Kaynaklara kimin, ne erişimi olduğunu kontrol eder.  
"En az yetki" prensibiyle çalışır.

### 🎯 3 Temel Kavram:

|Kavram|Açıklama|
|---|---|
|**Security Principal**|Kullanıcı, grup, servis hesabı|
|**Role Definition**|Ne yapabilir? (Reader, Contributor...)|
|**Scope**|Nerede? (Resource → RG → Subscription)|

---
### 📦 Yaygın Roller:

|Rol|Yetki Açıklaması|
|---|---|
|Owner|Tüm haklara sahip|
|Contributor|Tüm kaynakları yönetir, siler|
|Reader|Salt okunur|
|User Access Admin|RBAC yönetimi|

---
### 🔐 4. Rol Atama Örneği (RBAC)
```bash
az role assignment create \
  --assignee ahmet@mydomain.onmicrosoft.com \
  --role "Reader" \
  --scope /subscriptions/{subId}/resourceGroups/myRG
```
---
## 🔐 5. Managed Identity

Uygulamalara kimlik atamaktır. Şifre olmadan, uygulama Azure kaynaklarına güvenli şekilde erişebilir.

|Tür|Açıklama|
|---|---|
|**System Assigned**|Kaynakla birlikte oluşturulur|
|**User Assigned**|Birden fazla kaynakta paylaşılabilir|

---
## 🔑 6. Azure Key Vault ile Erişim

*Managed Identity veya RBAC ile Key Vault gibi gizli bilgi saklanan kaynaklara erişim sağlanabilir.*
```bash
az keyvault set-policy \
  --name myKeyVault \
  --object-id <principalId> \
  --secret-permissions get list
```
---
## 🔄 7. Azure AD vs RBAC

|Özellik|Azure AD|RBAC|
|---|---|---|
|Kimlik yönetimi|Kullanıcı, grup, uygulama|Yok|
|Kaynak yönetimi|Yok|Azure kaynaklarına erişim|
|Uygulama erişimi|Evet|Hayır|

---
## 🧪 Güvenlik Pratikleri

- MFA (Multi-Factor Authentication) zorunlu hale getirilmeli
- RBAC ile "least privilege" prensibi uygulanmalı
- Servis bağlantıları sadece gerektiği kadar erişim ile sınırlandırılmalı

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/)
- [https://learn.microsoft.com/en-us/azure/role-based-access-control/](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
- [https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/)