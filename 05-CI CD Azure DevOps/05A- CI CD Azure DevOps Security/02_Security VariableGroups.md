# 🔐 Azure DevOps – Variable Groups ile Güvenli Değişken Yönetimi

## 🧠 Amaç

Pipeline’larda ortak kullanılan değişkenleri merkezi olarak tanımlamak ve gizli bilgileri güvenli bir şekilde yönetmek.

---
## 🔍 Variable Group Nedir?

- Azure DevOps Library altında tanımlanır.
- Birden fazla pipeline içinde aynı değişkenlerin kullanılmasına olanak tanır.
- Secrets (gizli) olarak işaretlenmiş değişkenlerle şifre gibi kritik bilgiler korunabilir.

---
## 🧱 Neden Kullanılır?

| Senaryo                              | Açıklama |
|--------------------------------------|----------|
| Ortak DB bağlantısı                  | `dbHost`, `dbUser`, `dbPassword` gibi değerler tüm pipeline’larda merkezi yönetilir |
| API anahtarları                      | Üçüncü parti servislerdeki token veya key bilgileri |
| Ortam bazlı yapılandırma            | `env=dev`, `env=prod` gibi değişkenlerle ortam farkı ayarlanır |

---
## 🛠️ Variable Group Oluşturma

Azure DevOps Portal üzerinden:

1. Pipelines > Library > Variable Groups > `+ Variable Group`
2. Ad ver, değişkenleri ekle
3. Gizli değişken için `Keep this value secret` seçeneğini işaretle
4. “Allow access to all pipelines” kutusunu işaretleyebilirsin (isteğe bağlı)

---
## 🧪 YAML Pipeline'da Kullanımı

```yaml
variables:
  - group: prod-variables

steps:
  - script: echo "Production DB Host: $(dbHost)"
```

*Burada `prod-variables` adındaki variable group içerisindeki tüm değişkenler bu pipeline’da kullanılır hale gelir.*

---
## 🔐 Secret Değişken Kullanımı

Secret olarak işaretlenen değişkenler:

- Pipeline log’larında sansürlenir (***)
- Environment değişkeni olarak iletilebilir
- Kod içinde doğrudan kullanılmamalıdır

```yaml
steps:
  - script: echo "Deploying to $(envName)"
  - script: echo "Password is hidden"
    env:
      PASSWORD: $(dbPassword)   # Secret değişken
```

---
## ⚠️ İzin ve Erişim Kontrolü

- Variable group sadece yetkili pipeline’larda erişilebilir olmalı
- Her pipeline’ın variable group erişimi ayrı ayrı kontrol edilmelidir
- RBAC (Role-Based Access Control) ile kim, hangi değişkeni görebilir belirlenmelidir

---
## 💡 İpuçları

- Ortam bazlı variable group oluştur: `dev-variables`, `prod-variables`
- Birden çok variable group aynı pipeline’da kullanılabilir
- Variable değerlerini dışarıdan JSON dosyasıyla da güncelleyebilirsin (API destekli)

---

## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables)