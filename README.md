# Kafka + UI with Docker Compose

Setup ini menggunakan **Apache Kafka Native** (resmi dan ringan) dan **Kafdrop** (UI untuk memantau topic).  
Konfigurasi sudah mendukung akses:

- **Internal antar service** dalam Docker network  
- **Internal di dalam satu host (di luar container)**  
- **External (internet)** melalui satu port (9092)  

---

## 🚀 Structure

- `docker-compose.yml` → definisi service Kafka & UI  
- `.env.local` → konfigurasi untuk environment lokal  
- `.env.server` → konfigurasi untuk server  

---

## ⚙️ Config Env

### 🔹 `.env.local` (untuk development di laptop)
```env
PUBLIC_IP=localhost
```

### 🔹 `.env.ec2` (untuk deploy di server)
```env
PUBLIC_IP=<YOUR_PUBLIC_IP>   # atau domain name
```

---

## ▶️ Cara Menjalankan

### 1. Jalankan di Local
```bash
docker compose --env-file .env.local up -d
```
- Kafka tersedia di `localhost:9092`  
- UI (Kafdrop) tersedia di [http://localhost:9000](http://localhost:9000)  

### 2. Jalankan di server
```bash
docker compose --env-file .env.server up -d
```
- Kafka bisa diakses dari:
  - **Dalam Docker network:** `kafka:29092`  
  - **Dari host EC2:** `localhost:9092`  
  - **Dari internet:** `<YOUR_PUBLIC_IP>:9092`  
- UI (Kafdrop) tersedia di `http://<YOUR_PUBLIC_IP>:9000`  

---

## 🔎 Note

- `KAFKA_AUTO_CREATE_TOPICS_ENABLE=true` → Topic otomatis dibuat saat dipakai producer/consumer.
- Untuk production disarankan:
  - Menonaktifkan `KAFKA_AUTO_CREATE_TOPICS_ENABLE`  
  - Menambahkan konfigurasi `log.retention.hours`, `num.partitions`, dll sesuai kebutuhan workload.  

---
