## 🎯 Senaryo:

Bir web uygulamamız var. Uygulama Azure Web App’e deploy edilecek. Build sonrası test çalışacak ve başarılıysa Azure’a gönderilecek.

### 🔧 Ön Koşullar:

- Azure Resource Manager bağlantısı: `MyAzureConnection`
- Azure Web App adı: `my-webapp-demo`
- Uygulama framework: .NET Core 7.0 veya benzeri

---
### 📄 azure-pipelines.yml
```yaml
trigger:
  branches:
    include:
      - main

pool:
  vmImage: 'ubuntu-latest'

variables:
  buildConfiguration: 'Release'

stages:

# 👷 Build ve Test
- stage: BuildAndTest
  displayName: 'Build and Run Tests'
  jobs:
    - job: Build
      steps:
        - task: UseDotNet@2
          inputs:
            packageType: 'sdk'
            version: '7.x'
        
        - script: dotnet restore
          displayName: 'Restore Dependencies'

        - script: dotnet build --configuration $(buildConfiguration)
          displayName: 'Build Project'

        - script: dotnet test --configuration $(buildConfiguration) --logger:trx
          displayName: 'Run Unit Tests'

        - task: PublishTestResults@2
          inputs:
            testResultsFiles: '**/*.trx'
            testRunTitle: 'Test Results'

        - script: dotnet publish -c $(buildConfiguration) -o $(Build.ArtifactStagingDirectory)
          displayName: 'Publish Build Output'

        - task: PublishBuildArtifacts@1
          inputs:
            pathToPublish: '$(Build.ArtifactStagingDirectory)'
            artifactName: 'drop'
            publishLocation: 'Container'

# 🚀 Deploy
- stage: Deploy
  displayName: 'Deploy to Azure'
  dependsOn: BuildAndTest
  condition: succeeded()

  jobs:
    - deployment: DeployWebApp
      environment: 'Production'
      strategy:
        runOnce:
          deploy:
            steps:
              - download: current
                artifact: drop

              - task: AzureWebApp@1
                inputs:
                  azureSubscription: 'MyAzureConnection'
                  appName: 'my-webapp-demo'
                  package: '$(Pipeline.Workspace)/drop'
```
## 🧠 Açıklamalar:

|Satır|Anlamı|
|---|---|
|`trigger`|main branch'e her push sonrası pipeline otomatik çalışır.|
|`UseDotNet`|Pipeline agent’ına gerekli .NET SDK kurulumu yapılır.|
|`dotnet publish`|Yayına hazır hale getirilen dosyalar çıkartılır.|
|`PublishBuildArtifacts`|Bu çıktılar release aşaması için kaydedilir.|
|`AzureWebApp`|Azure Web App üzerine deploy işlemi yapılır.|

---
## ✅ Özelleştirme Önerileri

- Node.js/Nginx için farklı image ve script adımları kullanılabilir.
- `preDeployApprovals` veya `ManualValidation` adımı eklenebilir.
- Farklı environment (Staging, QA, Prod) için `multi-stage` pipeline yapılabilir.