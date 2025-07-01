# 🤖 Kubernetes Operators – Otomasyon ve Özelleştirilmiş Yönetim

## 🧠 Amaç

Kubernetes üzerinde karmaşık uygulamaların ve durum yönetiminin otomatikleştirilmesi için Operator kavramını öğrenmek.

---
## 🤔 Operator Nedir?

- Kubernetes kaynaklarını yönetmek için özel kontrol döngüsü (controller) içeren yazılım.
- İnsan müdahalesi olmadan uygulamaların kurulumu, güncellenmesi ve yönetimini sağlar.
- Örneğin, veri tabanı kümelerinin otomatik kurulumu ve ölçeklendirilmesi.

---
## 🔧 Operator Bileşenleri

| Bileşen           | Açıklama                            |
|-------------------|-----------------------------------|
| **Custom Resource Definition (CRD)** | Yeni kaynak tipleri tanımlanır. |
| **Controller**    | CRD için istenen durumu sağlar ve yönetir. |

---
## 🛠️ CRD Örneği (Basit)

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: databases.example.com
spec:
  group: example.com
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                size:
                  type: integer
  scope: Namespaced
  names:
    plural: databases
    singular: database
    kind: Database
    shortNames:
    - db
```
## 🔍 Operator Kullanımı

- CRD ile yeni kaynak tanımlanır.
- Operator controller bu kaynağı izler ve istenen durumu uygular.
- Örneğin, `Database` kaynağı oluşturunca otomatik pod, service vs. kurar.

---
## 🧰 Operator SDK

- Operator geliştirmek için kullanılan araç seti.
- Go, Ansible, Helm tabanlı operatorlar oluşturulabilir.

---
## 💡 İpuçları

- Karmaşık uygulamalar için yaşam döngüsü yönetimini kolaylaştırır.
- RedHat OpenShift ve diğer platformlarda sıkça kullanılır.
- Öğrenmek için basit operator örnekleriyle başlamak faydalı.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/extend-kubernetes/operator/
- https://sdk.operatorframework.io/