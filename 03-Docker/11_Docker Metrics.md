# 📊 Docker Metrics (İzleme ve Kaynak Kullanımı)

## 🧠 Amaç

Container'ların CPU, bellek ve disk kullanımlarını izlemek, performans sorunlarını tespit edebilmek.

---

## 🛠️ Temel Komutlar

### 🔹 Canlı İzleme
```bash
docker stats
```
## 🔹 Kaynak Sınırları Verme
```bash
docker run -d \
  --name sınırtesti \
  --memory="512m" \
  --cpus="1.0" \
  nginx
```
*Bellek ve işlemci limiti verir.*

# 📈 Gelişmiş İzleme Araçları
## 🟦 1. cAdvisor (Google)
```bash
docker run \
  -d \
  -p 8080:8080 \
  --name=cadvisor \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:ro \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  gcr.io/cadvisor/cadvisor
```
*Web arayüzü ile container'ları anlık izleme.*
### 📦 2. Prometheus + Grafana

- Prometheus container metrics çeker
- Grafana, bu metrikleri görselleştirir
- cAdvisor veya node-exporter gibi exporter’lardan veri alır
### 🔧 3. Docker Events
```bash
docker events
```
*Sistem düzeyinde her olayın canlı log’unu verir (start, stop, crash vs.)*
## 🧠 Best Practices

- Uzun çalışan projelerde `docker stats` yerine Prometheus veya Grafana entegrasyonu yapılmalı
- `--log-driver` ile loglama kontrol altına alınmalı (örn: `json-file`, `fluentd`)
- `--memory`, `--cpus` gibi sınırlar her prod container için zorunlu olmalı
## Kaynaklar

- https://docs.docker.com/config/containers/runmetrics/
- [https://github.com/google/cadvisor](https://github.com/google/cadvisor)
- https://prometheus.io/docs/
- [https://grafana.com/](https://grafana.com/)