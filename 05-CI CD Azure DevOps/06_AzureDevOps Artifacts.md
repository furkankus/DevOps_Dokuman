# 📦 Azure DevOps Artifacts – Paket ve Bağımlılık Yönetimi

## 🧠 Amaç

Azure DevOps Artifacts kullanarak uygulama paketlerini yönetmeyi, paylaşmayı ve CI/CD süreçlerine entegre etmeyi öğrenmek.

---
## 🔍 Azure Artifacts Nedir?

- NuGet, npm, Maven, Python ve Universal paketler için özel bir paket besleme (feed) sistemidir.
- Kütüphanelerinizi versiyonlanabilir ve paylaştırılabilir hale getirir.
- Yayınlanan paketleri build pipeline'dan release pipeline’a geçirebilirsiniz.

---
## 🧱 Azure Artifacts Bileşenleri

| Bileşen    | Açıklama |
|------------|----------|
| **Feed**   | Paketlerin saklandığı yer |
| **Upstream Sources** | Harici kaynaklardan (örn. NuGet.org) paket çekmeyi sağlar |
| **Scoped Permissions** | Feed'e erişim yetkileri belirlenebilir |
| **Retention Policies** | Eski versiyon paketlerin otomatik silinmesi |

---
## 🛠️ Feed Oluşturma

1. Azure DevOps > Artifacts > New Feed
2. Feed ismini gir (örn. `MyCompany.Packages`)
3. Erişim türünü belirle (public, project scoped, org scoped)
4. Gerekirse upstream kaynakları aktif et (örn. `https://registry.npmjs.org`)

---
## 📝 NuGet Paketi Yayınlama (dotnet örneği)
```bash
dotnet pack MyLibrary.csproj -o ./output
dotnet nuget push ./output/MyLibrary.1.0.0.nupkg \
  --source "https://pkgs.dev.azure.com/{organization}/{project}/_packaging/{feed}/nuget/v3/index.json" \
  --api-key az
```
*`az artifacts universal publish` komutu ile universal paket de yüklenebilir.*

---
## 📦 Paketleri Pipeline’da Kullanmak
### 1. Build Pipeline’da Paket Yayınlama:
```yaml
- task: NuGetCommand@2
  inputs:
    command: 'push'
    packagesToPush: '**/*.nupkg'
    publishVstsFeed: 'your-feed-id-or-name'
```
### 2. Build Pipeline’da Paket Kullanma:
```yaml
- task: NuGetCommand@2
  inputs:
    command: 'restore'
    feedsToUse: 'select'
    vstsFeed: 'your-feed-id-or-name'
```
---
## 💡 İpuçları

- Dahili kütüphaneleri feed içinde tutmak versiyon ve bağımlılık kontrolünü kolaylaştırır.
- Her ortam için farklı feed kullanabilirsin (örn. dev-feed, prod-feed).
- `Universal Packages` binary dosyalar için iyi bir seçenektir.

---
## 🔐 Güvenlik

- Feed bazlı okuma-yazma izinleri verilebilir.
- Feed’leri sadece belirli gruplarla paylaşabilirsin.
- Feed’e erişen servis bağlantılarına özel erişim belirlenebilir.

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/artifacts/overview](https://learn.microsoft.com/en-us/azure/devops/artifacts/overview)
- [https://learn.microsoft.com/en-us/azure/devops/artifacts/quickstarts](https://learn.microsoft.com/en-us/azure/devops/artifacts/quickstarts)