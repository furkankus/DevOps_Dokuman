# ☸️ Kubernetes'e Giriş

## 🧠 Amaç

Uygulamaları otomatik, esnek ve yüksek erişilebilirlikte çalıştırmak için Kubernetes'in temel yapı taşlarını ve genel mantığını öğrenmek.

---
## 🧩 Temel Bileşenler

| Bileşen     | Açıklama |
|-------------|----------|
| **Pod**     | En küçük çalışma birimi. İçinde bir veya daha fazla container barındırabilir. |
| **Node**    | Uygulamaların çalıştığı sunucu (VM ya da fiziksel makine). Worker veya Master olabilir. |
| **Cluster** | Birden fazla node’un birleşmesiyle oluşur. |
| **Deployment** | Uygulama versiyonlarını, replikasyonları ve rollout sürecini yönetir. |
| **Service** | Pod’lara stabil erişim sağlar (IP’ler değişse bile). |
| **Namespace** | Kaynakları gruplamak ve izole etmek için kullanılır. |
| **ConfigMap** | Ortam değişkenleri gibi yapılandırma ayarlarını içerir. |
| **Secret**   | Şifre ve hassas bilgiler için kullanılır. |

---
## 🖼️ Kubernetes Mimarisi

```plaintext
[User]
  │
  ▼
[Master Node]  -->  API Server, Scheduler, Controller, etcd
  │
  ▼
[Worker Nodes] -->  Kubelet + Container Runtime + Pod
```
## 🔁 Kubernetes Nasıl Çalışır?

1. **Kullanıcı** `kubectl apply -f` ile bir YAML dosyası gönderir.
2. **API Server** isteği alır, doğrular.
3. **Scheduler**, workload’u uygun bir node’a atar.
4. **Kubelet**, container’ları başlatır.
5. **Service**, dış dünyadan erişim sağlar.

## 📦 Kubernetes’in Sağladıkları

- ✅ **Otomatik Dağıtım ve Geri Alma (Rollback)**
- ✅ **Self-healing** (Pod çökerse otomatik yenisi başlatılır)
- ✅ **Otomatik Yük Dengeleme**
- ✅ **Yatay Ölçekleme (Scale Out/In)**
- ✅ **Konfigürasyon Yönetimi**
- ✅ **Storage Bağlama (PVC/PV)**

## ⚡ Temel Kavramlar Özet

|Terim|Tanım|
|---|---|
|Pod|Container kümesi (aynı IP ve volume paylaşırlar)|
|Node|Pod’ların çalıştığı fiziksel/VM sunucu|
|Deployment|Pod’ları yönetir, sürüm kontrolü yapar|
|ReplicaSet|Belirli sayıda pod’un hep çalışmasını sağlar|
|Service|Pod'lara sabit erişim noktası|
|ConfigMap/Secret|Ortam ayarlarını ve şifreleri dışa taşır|
|Namespace|Kaynakları mantıksal olarak ayırır|
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/
- [https://learnk8s.io/](https://learnk8s.io/)
- [https://kubernetesbyexample.com/](https://kubernetesbyexample.com/)