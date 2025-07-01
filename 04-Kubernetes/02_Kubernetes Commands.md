# 🧪 Kubernetes Komutları (`kubectl`)

## 🧠 Amaç

Kubernetes kaynaklarını yönetmek, uygulamaları dağıtmak ve sorunları teşhis etmek için gerekli `kubectl` komutlarını öğrenmek.

---

## 📂 Genel Kaynak Listeleme

```bash
kubectl get nodes                  # Node listesini göster
kubectl get pods                   # Pod listesini göster (default namespace)
kubectl get pods -n <namespace>   # Belirli namespace içindeki pod’lar
kubectl get all                   # Tüm kaynakları listele (pod, service, deployment, vs.)
kubectl get svc
```
## 🔍 Detayları Görüntüleme

```bash
kubectl describe pod <pod_ismi>       # Pod detayları 
kubectl describe service <svc_ismi>   # Service detayları 
kubectl describe deployment <name>    # Deployment detayları  
kubectl logs <pod_ismi>               # Pod loglarını göster 
kubectl logs <pod_ismi> -c <container_ismi>  # Pod içindeki spesifik container logu`
```
# ⚙️ YAML Dosyası Uygulama ve Silme
```bash
kubectl apply -f dosya.yml           # Kaynakları oluştur/güncelle
kubectl delete -f dosya.yml          # YAML ile oluşturulan kaynağı sil
kubectl apply -k ./klasor            # Kustomize yapılarını uygula
```
# 🧱 Pod ve Container İşlemleri
```bash
kubectl exec -it <pod_ismi> -- sh         # Pod içinde shell’e gir
kubectl exec -it <pod_ismi> -c <container_ismi> -- bash

kubectl port-forward <pod_ismi> 8080:80   # Pod’un 80 portunu local 8080’e yönlendir
```
# 📦 Kaynak Oluşturma (Komutla)
```bash
kubectl create deployment web --image=nginx
kubectl expose deployment web --port=80 --type=NodePort
kubectl scale deployment web --replicas=3
kubectl delete deployment web
```
# 📌 Namespace İşlemleri
```bash
kubectl get namespaces
kubectl create namespace deneme
kubectl delete namespace deneme
kubectl get pods -n deneme
```
# 🛠️ Yapılandırma ve Erişim
```bash
kubectl config view                # Aktif config dosyasını göster
kubectl config get-contexts        # Bağlı olduğun cluster’lar
kubectl config use-context <ad>    # Cluster değiştir
```
# 🚨 Sorun Giderme Komutları
```bash
kubectl describe pod <isim>        # Etkin olayları (Events) gösterir
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get pod <isim> -o yaml     # YAML çıktısı al
```
## 🧠 İpuçları

- `-o wide` ➤ Ek bilgi gösterir (IP, node vb.)
- `-A` ➤ Tüm namespace’lerde arama yapar
- `--dry-run=client -o yaml` ➤ Kaynağı oluşturmaz, YAML çıktısı üretir
```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx-pod.yaml
```
## 🔗 Kaynaklar

- https://kubernetes.io/docs/reference/kubectl/
- https://kubernetes.io/docs/tasks/debug/debug-cluster/