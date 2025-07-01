# 💾 Kubernetes Backup & Restore – Yedekleme ve Geri Yükleme

## 🧠 Amaç

Kubernetes cluster kaynakları ve persistent verilerin yedeklenmesi ve gerektiğinde geri yüklenmesini sağlamak.

---
## 🔍 Neden Yedekleme?

- Veri kaybı riskine karşı önlem
- Hatalı güncelleme ve silme durumunda geri dönüş
- Disaster Recovery (felaket kurtarma) planı

---
## 🛠️ Yedekleme Yapılacak Kaynaklar

- PersistentVolume (PV) ve PersistentVolumeClaim (PVC)
- Etcd (cluster state bilgisi)
- ConfigMap, Secret, Deployment, Service vs. YAML konfigürasyonları

---
## 🔧 Yedekleme Araçları

| Araç          | Açıklama                                 |
|---------------|------------------------------------------|
| **Velero**    | Popüler Kubernetes yedekleme ve geri yükleme aracı |
| **Etcdctl**   | Etcd veri tabanını yedeklemek için CLI araç |
| **Restic**    | Persistent volume snapshot’ları için alternatif |

---
## 📦 Velero Kurulumu

```bash
kubectl create namespace velero
velero install --provider aws --bucket <bucket-name> --secret-file ./credentials-velero --backup-location-config region=<region>
```
## 🔄 Yedekleme ve Geri Yükleme
```bash
# Yedekleme oluşturma
velero backup create my-backup

# Yedekten geri yükleme
velero restore create --from-backup my-backup
```
## 📝 Etcd Yedekleme
```bash
ETCDCTL_API=3 etcdctl snapshot save snapshot.db --endpoints=<etcd-endpoint> --cacert=<ca.crt> --cert=<client.crt> --key=<client.key>
```
## 💡 İpuçları

- Yedeklerinizi düzenli test edin.
- Kritik veriler için farklı lokasyonlarda yedek tutun.
- Otomatik yedekleme planları yapın.

---
## 🔗 Kaynaklar

- https://velero.io/docs/
- https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/