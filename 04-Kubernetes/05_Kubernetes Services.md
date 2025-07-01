# 🔌 Kubernetes Services – Ağ Erişimi ve Yük Dengeleme

## 🧠 Amaç

Pod’ların IP adresleri dinamik olduğu için, pod’lara sabit ve güvenilir erişim sağlamak için Service kavramını öğrenmek.

---
## 🧩 Service Nedir?

- Pod’lara dışarıdan veya cluster içinden erişim için soyutlama katmanı.
- Pod IP’leri değişse bile sabit bir IP veya DNS sağlar.
- Farklı türleri vardır: ClusterIP, NodePort, LoadBalancer, ExternalName.

---
## 🛠️ Service Türleri

| Tür           | Açıklama                                      | Kullanım Alanı                          |
|---------------|-----------------------------------------------|---------------------------------------|
| **ClusterIP** | En yaygın, sadece cluster içinden erişim sağlar. | Servisler arası iletişim               |
| **NodePort**  | Her node’un belirli portunu açar, dış erişim sağlar. | Geliştirme veya basit dış erişim      |
| **LoadBalancer** | Bulut sağlayıcıların LB servisini kullanır, dış erişim için IP verir. | Prod ortam, yüksek erişilebilirlik    |
| **ExternalName** | DNS ismi ile başka bir servise yönlendirir. | Servis keşfi, DNS bazlı yönlendirme  |

---
## 📄 Örnek ClusterIP Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP
```
## 📄 Örnek NodePort Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30007  # 30000-32767 arası seçilebilir
```
## 🔍 Açıklamalar

- `selector`: Hangi pod’ların bu servise dahil olduğu
- `port`: Servisin dışarıya açtığı port
- `targetPort`: Pod içindeki container’ın portu
- `nodePort`: Dış erişim için node üzerindeki port (NodePort tipi için)

---

## 🧩 Service ve DNS

- Kubernetes, servis isimlerini otomatik DNS olarak çözer.
- Örneğin `my-service` servisine cluster içinden 
	-`my-service.namespace.svc.cluster.local` ile erişilir.

---
## 🧪 Service Oluşturma ve Yönetimi
```bash
kubectl apply -f service.yaml
kubectl get svc
kubectl describe svc my-service
kubectl delete svc my-service
```
## 💡 İpuçları

- Prod ortamda genellikle LoadBalancer tipi kullanılır.
- NodePort sadece küçük ve lokal testler için uygundur.
- Service olmadan pod’lar doğrudan dışarı erişilebilir olmaz.

---
## 🔗 Kaynaklar

- https://kubernetes.io/docs/concepts/services-networking/service/
	- https://kubernetes.io/docs/tutorials/services/source-ip/