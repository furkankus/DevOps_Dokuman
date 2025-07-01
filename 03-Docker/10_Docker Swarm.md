# 🐝 Docker Swarm (Dağıtık Orkestrasyon)

## 🧠 Amaç

Birden fazla sunucudan oluşan dağıtık bir sistemde container'ları yönetmek, yüksek erişilebilirlik ve ölçeklenebilirlik sağlamak.

---

## ⚙️ Swarm Nedir?

Docker Swarm, birden çok Docker host’unu (sunucusunu) tek bir cluster gibi yöneten yerleşik bir orkestrasyon çözümüdür.

---

## 🛠️ Swarm Yapılandırması

### 🔹 Swarm Başlatma
```bash
docker swarm init
```
*Çalıştığın makine **manager** node olur.*

### 🔹 Worker Node'ları Ekleme
```bash
#Manager node'da token al: 
docker swarm join-token worker  
#Worker node’da çalıştır: 
docker swarm join --token <token> <manager-ip>:2377`
```
# 🧱 Servis Oluşturma
```bash
docker service create \
  --name web \
  --replicas 3 \
  -p 80:80 \
  nginx
```
*Bu komut, 3 tane nginx container'ı cluster’da dağıtır.*
## 🔹 Servisleri Görüntüleme
```bash
docker service ls
docker service ps web
```
## 🔹 Ölçeklendirme
```bash
docker service scale web=5
```
# 🌐 Overlay Network ile Hostlar Arası İletişim
```bash
docker network create --driver overlay mynet
```
*Container’lar farklı makinelerde olsa bile bu ağda birbirine ulaşabilir.*
## 🛑 Swarm'dan Çıkmak
```bash
docker swarm leave --force  # Manager
docker swarm leave          # Worker
```
## ❗️Dikkat Edilecek Noktalar

- `docker-compose.yml` dosyası `deploy` alanı ile Swarm’a uyarlanabilir
- Swarm, Kubernetes kadar güçlü değildir ancak daha basittir
- Overlay network olmazsa node’lar arası container iletişimi mümkün değildir
---
## 🔗 Kaynaklar

- https://docs.docker.com/engine/swarm/
- https://dockerlabs.collabnix.com/swarm/
- [https://github.com/dockersamples/example-voting-app](https://github.com/dockersamples/example-voting-app) – Örnek proje