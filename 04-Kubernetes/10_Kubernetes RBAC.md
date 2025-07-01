	# 🛡️ Kubernetes RBAC – Yetkilendirme ve Erişim Kontrolü

## 🧠 Amaç

Kubernetes cluster’ında kullanıcıların ve servis hesaplarının (service accounts) erişim yetkilerini rol tabanlı olarak yönetmeyi öğrenmek.

---
## 🔑 RBAC Nedir?

- Role-Based Access Control (RBAC), yetki yönetimi sistemidir.
- Kullanıcılara veya servis hesaplarına belirli kaynaklar üzerinde belirli izinler verilir.
- İzinler Role veya ClusterRole objeleri ile tanımlanır.
- Bu roller RoleBinding veya ClusterRoleBinding ile kullanıcı/hesaplara atanır.

---
## 🎯 Temel Kaynaklar

| Kaynak            | Açıklama                           |
|-------------------|----------------------------------|
| **Role**          | Belirli namespace içinde yetki tanımı |
| **ClusterRole**   | Cluster çapında yetki tanımı      |
| **RoleBinding**   | Role’u namespace içindeki kullanıcıya bağlar |
| **ClusterRoleBinding** | ClusterRole’ü tüm cluster’da kullanıcıya bağlar |

---
## 🔧 Örnek Role
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]  # Core API Group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```
## 🔧 Örnek RoleBinding
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: default
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
## 🔍 Örnek ClusterRole ve ClusterRoleBinding
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-admin
rules:
- apiGroups: ["*"]
  resources: ["*"]
  verbs: ["*"]
```
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-binding
subjects:
- kind: User
  name: admin-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```
## ⚙️ RBAC Yönetimi Komutları
```bash
kubectl get roles -n default
kubectl get rolebindings -n default
kubectl get clusterroles
kubectl get clusterrolebindings
```
## 💡 İpuçları

- İzinleri mümkün olduğunca “least privilege” prensibine göre ver.
- ClusterRole ve ClusterRoleBinding daha geniş yetkiler içindir, dikkatli kullan.
- Servis hesapları (service accounts) için de RBAC tanımları yapılabilir.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/reference/access-authn-authz/rbac/
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/