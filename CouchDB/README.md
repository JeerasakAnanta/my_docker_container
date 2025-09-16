# 📘 การติดตั้ง Apache CouchDB ด้วย Docker Compose

## ✅ ความต้องการเบื้องต้น
ก่อนติดตั้ง ตรวจสอบให้แน่ใจว่ามีเครื่องมือดังนี้
- [Docker](https://docs.docker.com/get-docker/)  
- [Docker Compose](https://docs.docker.com/compose/install/)  

---

## 🚀 ขั้นตอนการติดตั้ง CouchDB

### 1. สร้างไฟล์ `docker-compose.yml`
```yaml
version: "3.9"

services:
  couchdb:
    image: couchdb:3.3
    container_name: couchdb
    restart: unless-stopped
    ports:
      - "5984:5984" # CouchDB Web UI / API
    environment:
      - COUCHDB_USER=admin
      - COUCHDB_PASSWORD=admin123
    volumes:
      - couchdb_data:/opt/couchdb/data

volumes:
  couchdb_data:
````

---

### 2. รัน CouchDB

เปิด Terminal และสั่งรัน

```bash
docker-compose up -d
```

ตรวจสอบ container

```bash
docker ps
```

---

### 3. เข้าใช้งาน CouchDB

เปิดเบราว์เซอร์ไปที่
👉 [http://localhost:5984/\_utils](http://localhost:5984/_utils)

เข้าสู่ระบบด้วย

* **Username:** `admin`
* **Password:** `admin123`

---

### 4. โครงสร้างข้อมูล

* CouchDB เก็บข้อมูลเป็น **Database** → **Document (JSON)**
* สามารถเรียกใช้ผ่าน **REST API** เช่น

```bash
curl http://admin:admin123@localhost:5984/_all_dbs
```

---

## 🔧 คำสั่งที่ใช้บ่อย

* หยุด container

  ```bash
  docker-compose down
  ```
* ดู logs

  ```bash
  docker logs couchdb
  ```
* ลบข้อมูลทั้งหมด

  ```bash
  docker volume rm <project_name>_couchdb_data
  ```

---

## 📌 สรุป

* ติดตั้งง่ายผ่าน Docker Compose
* ใช้งานผ่าน **Fauxton UI** ที่ `http://localhost:5984/_utils`
* เหมาะสำหรับ **Offline-first applications**, **Distributed systems**, และ **IoT**

---
