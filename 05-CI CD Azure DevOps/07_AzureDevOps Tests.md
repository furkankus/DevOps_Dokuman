# ✅ Azure DevOps Tests – Otomatik Test Entegrasyonu

## 🧠 Amaç

Build ve release süreçlerine test adımlarını entegre ederek kod kalitesini artırmayı ve test sonuçlarını raporlamayı öğrenmek.

---
## 🔍 Neden Otomatik Test?

- Hataları erken tespit etme
- Kod kalitesini koruma
- Sürekli entegrasyonun vazgeçilmez parçası
- Geliştirme sürecine güven kazandırma

---
## 🧪 Test Türleri

| Tür             | Açıklama                           |
|------------------|------------------------------------|
| **Unit Test**    | Fonksiyonların küçük parçalarının testi |
| **Integration Test** | Bileşenlerin bir arada çalışmasının testi |
| **UI/Functional Test** | Gerçek kullanıcı etkileşimlerinin testi |
| **Load/Performance Test** | Sistem kapasite testi |

---
## 🛠️ YAML ile Test Entegrasyonu (Örnek: .NET)

```yaml
- script: dotnet test --logger:trx
  displayName: 'Run Tests'

- task: PublishTestResults@2
  inputs:
    testResultsFiles: '**/*.trx'
    testRunTitle: 'Test Results'
```
## 🛠️ YAML ile Test Entegrasyonu (Örnek: JavaScript)
```yaml
- script: |
    npm install
    npm test -- --ci --reporters=jest-junit
  
- displayName: 'Run JS Tests'

- task: PublishTestResults@2
  inputs:
    testResultsFiles: '**/junit.xml'
    testRunTitle: 'Jest Test Results'

```
---
## 🧾 Test Sonuçlarını Yayınlama

- `PublishTestResults@2` task’ı ile Azure DevOps portalına test sonuçları gönderilir.
- “Tests” sekmesinden başarı/başarısız test detayları görülür.
- Hatalı testler grafiksel olarak raporlanır.
---
### 📊 Code Coverage (Kapsam) Raporu Yayınlama
```yaml
- task: DotNetCoreCLI@2
  inputs:
    command: 'test'
    projects: '**/*Tests.csproj'
    arguments: '--collect:"Code Coverage"'
```
*Sonrasında **"Code Coverage Results"** sekmesinde kapsam bilgisi raporlanır.*

---
## 🔄 Release Pipeline’da Test Çalıştırma

- Smoke test, UI test, post-deploy script gibi işlemler yapılabilir.
- Ortama deploy sonrası doğrulama için kullanılır.
```yaml
- task: AzureCLI@2
  inputs:
    scriptType: 'bash'
    scriptLocation: 'inlineScript'
    inlineScript: 'curl -f https://your-app-url/health'
```

---
## 💡 İpuçları

- Her PR veya merge işlemi öncesi test çalıştırmak güvenlik sağlar.
- Test başarısızsa build’i durdur.
- Raporlar sayesinde ekip üyeleri anında hata takibi yapabilir.

---
## 🔗Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/pipelines/test/](https://learn.microsoft.com/en-us/azure/devops/pipelines/test/)
- [https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/test/publish-test-results](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/test/publish-test-results)