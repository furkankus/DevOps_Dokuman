# 🏗️ Azure DevOps Builds – Derleme ve Artifact Üretimi

## 🧠 Amaç

Azure DevOps’ta build (derleme) pipeline’larının ne işe yaradığını, nasıl oluşturulduğunu ve çıktılarının nasıl kullanıldığını öğrenmek.

---
## 🔍 Build Pipeline Nedir?

- Kodun derlenmesi, test edilmesi ve deploy edilebilir hale getirilmesi sürecidir.
- Genellikle CI sürecinin ilk ve en temel parçasıdır.
- Çıktı olarak **artifact** (örneğin: .jar, .zip, .dll, .img) üretir.

---
## 🔧 Build Pipeline Ne Yapar?

| Adım             | Açıklama |
|------------------|----------|
| **Restore**      | Bağımlılıkların yüklenmesi (örn. `npm install`, `dotnet restore`) |
| **Build**        | Kodun derlenmesi |
| **Test**         | Birim testlerin çalıştırılması |
| **Publish**      | Artifact’ın üretilip dışa aktarılması |
| **Upload**       | Artifact’ın Azure DevOps üzerinde saklanması |

---
## 📄 Basit Build Pipeline Örneği

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

steps:
  - task: UseDotNet@2
    inputs:
      packageType: 'sdk'
      version: '7.x'

  - script: dotnet restore
    displayName: 'Restore dependencies'

  - script: dotnet build --configuration Release
    displayName: 'Build'

  - script: dotnet test
    displayName: 'Test'

  - script: dotnet publish -c Release -o $(Build.ArtifactStagingDirectory)
    displayName: 'Publish'

  - task: PublishBuildArtifacts@1
    inputs:
      pathToPublish: '$(Build.ArtifactStagingDirectory)'
      artifactName: 'drop'
```
## 🗂️ Artifact Nedir?

- Build sonucunda ortaya çıkan deploy edilebilir dosyadır.
- Bir sonraki aşamada (örneğin: release pipeline) kullanılır.
- Azure DevOps üzerinde “Artifacts” sekmesinde saklanır.

---
## 📦 Build Pipeline ile Artifact Yayınlama
```yaml
  - task: PublishBuildArtifacts@1
    inputs:
      pathToPublish: '$(Build.ArtifactStagingDirectory)'
      artifactName: 'drop'
```
*Yukarıdaki adım, build edilen dosyaları yayınlayarak bir "drop" adlı artifact haline getirir.*

---
## 🧪 Test Entegrasyonu

- Test adımlarında `dotnet test`, `npm test`, `pytest` gibi komutlar kullanılır.
- Sonuçlar `PublishTestResults` task'ı ile saklanabilir.

---
## 💡 İpuçları

- Her build işlemi temiz bir ortamda çalışır.
- Build süresi uzun olan projelerde caching kullanmak süreyi azaltır.
- Artifact’lar versiyonlanarak saklanabilir (`v1.0.0`, `build-1234` gibi).

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/build/](https://learn.microsoft.com/en-us/azure/devops/pipelines/build/)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/artifacts/artifacts-overview](https://learn.microsoft.com/en-us/azure/devops/pipelines/artifacts/artifacts-overview)