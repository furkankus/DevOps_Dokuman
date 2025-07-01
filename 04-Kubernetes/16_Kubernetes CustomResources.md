# 🛠️ Kubernetes Custom Resources (CR) ve Custom Resource Definitions (CRD)

## 🧠 Amaç

Kubernetes’in standart kaynakları dışında kendi özel kaynak tiplerini tanımlayıp yönetmeyi öğrenmek.

---
## 🔑 CR ve CRD Nedir?

- **Custom Resource (CR):** Kullanıcının tanımladığı özel kaynak objesi.
- **Custom Resource Definition (CRD):** Kubernetes API’ye yeni kaynak tipi eklemek için kullanılan tanım.

---
## 🔧 CRD Oluşturma Örneği

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: foos.example.com
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
                bar:
                  type: string
  scope: Namespaced
  names:
    plural: foos
    singular: foo
    kind: Foo
    shortNames:
    - f
```
## 🔍 CR (Custom Resource) Örneği
```yaml
apiVersion: example.com/v1
kind: Foo
metadata:
  name: foo-sample
spec:
  bar: "Değer"
```
## 🛠️ Kullanım

- CRD tanımlandıktan sonra `kubectl get crd` ile yeni kaynak tipini görürsün.
- CR yaratıp, custom controller ile izlenebilir.
- Operatorlar genelde CRD ve CR kullanır.

---
## 💡 İpuçları

- CRD’ler Kubernetes API’yi genişletir.
- Kolayca yeni kaynak tipleri yaratıp otomasyon yapabilirsin.
- Karmaşık uygulamalar için ideal.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/
- https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/