# 🗂️ Azure DevOps Repos – Kod Deposu Yönetimi

## 🧠 Amaç

Azure DevOps Repos kullanarak kaynak kodlarının nasıl yönetildiğini, Git akışlarını ve temel repo işlemlerini öğrenmek.

---
## 🔍 Azure Repos Nedir?

Azure Repos, Git veya Team Foundation Version Control (TFVC) tabanlı kod depoları sağlar. Modern yazılım geliştirme süreçlerinde genellikle Git tercih edilir.

---
## 🚧 Git Akış Modelleri

- **GitHub Flow:** Main branch’e doğrudan merge
- **Git Flow:** `feature`, `develop`, `release`, `hotfix` dalları ile yönetim
- **Trunk-based development:** Tek ana daldan geliştirme, sık merge/push

Azure DevOps, tüm bu modelleri destekler.

---
## 🛠️ Azure Repos ile Yapabileceklerin

- Repository (repo) oluşturma
- Dallar (branch) oluşturma, birleştirme (merge)
- Pull Request (PR) açma ve kod inceleme
- Commit geçmişi izleme
- Branch politikaları tanımlama (örn. kodu merge etmeden önce onay gerekmesi)

---
## 🔧 Repo Oluşturma

1. Azure DevOps portalına gir.
2. Projeyi seç.
3. “Repos” sekmesine git.
4. “New repository” → `Git` veya `TFVC` türünü seç.
5. İsteğe bağlı olarak README ve `.gitignore` ekle.

---
## 📦 Pull Request Örneği

- `feature/login` dalında geliştirme yap.
- `main` dalına PR aç.
- Kod incelemesi ve onay (review) iste.
- Merge işlemini gerçekleştir.

---
## 🛡️ Branch Policies (Dal Politikaları)

| Politika                 | Açıklama |
|--------------------------|----------|
| **Reviewers**            | PR'lar için belirli kişi/ekip onayı gerekir |
| **Build Validation**     | PR merge edilmeden önce build geçmeli |
| **Work Item Linking**    | PR, görevle ilişkilendirilmiş olmalı |
| **Status Checks**        | Harici sistem doğrulamaları yapılmalı |

---
## 🔍 Kod Gözden Geçirme Süreci

- PR üzerinden yorum yapabilirsin.
- Satır bazında öneri bırakılabilir.
- Geliştirici geri dönüp düzenleme yapabilir.
- Onaylayan kişi merge işlemini başlatır.

---
## 💡 İpuçları

- Branch politikaları ile hatalı kodların ana dala girmesini engellersin.
- Geliştirme sürecini `feature/`, `bugfix/`, `hotfix/` dalları ile modüler yönet.
- Repo’ya erişim rollerini iyi yönet: Contributor, Reader, Administrator.

---
## 🔗 Kaynaklar

- [https://learn.microsoft.com/en-us/azure/devops/repos/](https://learn.microsoft.com/en-us/azure/devops/repos/)
- [https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-policies](https://learn.microsoft.com/en-us/azure/devops/repos/git/branch-policies)
	 