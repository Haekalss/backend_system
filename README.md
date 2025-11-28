# 🚀 GIS Backend API

Backend server untuk aplikasi Geographic Information System (GIS) menggunakan Express.js dan MongoDB.

## 📋 Prerequisites

- Node.js v18+
- MongoDB (local atau MongoDB Atlas)
- npm atau yarn

## 🚀 Setup & Run

### 1. Clone & Install

```bash
git clone https://github.com/violasptntels/Backend-Geographic-Information-System.git
cd Backend-Geographic-Information-System
npm install
```

### 2. Setup Environment

```bash
# Copy .env.example ke .env
cp .env.example .env

# Edit .env dengan konfigurasi Anda
# MONGODB_URI=mongodb://localhost:27017/gis_database
# PORT=3001
```

### 3. (Opsional) Import Sample Data

```bash
npm run import
```

### 4. Run Server

**Development:**
```bash
npm run dev
```

**Production:**
```bash
npm start
```

Server akan berjalan di port yang ditentukan di `.env` (default: 3001)

## 📡 API Endpoints

### Locations

| Method | Endpoint | Deskripsi |
|--------|----------|-----------|
| GET | `/api/locations` | Get semua lokasi |
| GET | `/api/locations?category=restaurant` | Filter by category |
| GET | `/api/locations?search=keyword` | Search lokasi |
| GET | `/api/locations/:id` | Get lokasi by ID |
| POST | `/api/locations` | Tambah lokasi baru |
| PUT | `/api/locations/:id` | Update lokasi |
| DELETE | `/api/locations/:id` | Hapus lokasi |

### Request Body (POST/PUT)

```json
{
  "name": "Restoran Sederhana",
  "category": "restaurant",
  "coordinates": {
    "lat": -6.200000,
    "lng": 106.816666
  },
  "address": "Jl. Contoh No. 123, Jakarta",
  "description": "Deskripsi lokasi",
  "rating": 4.5,
  "imageUrl": "https://example.com/image.jpg"
}
```

## 🏗️ Struktur Project

```
Backend-Geographic-Information-System/
├── server/
│   ├── index.js           # Server utama
│   ├── models/
│   │   └── Location.js    # MongoDB Schema
│   └── routes/
│       └── locations.js   # API Routes
├── import-data.js         # Script import sample data
├── package.json
├── .env.example
└── README.md
```

## 🗄️ Database Schema

**Location Model:**
```javascript
{
  _id: ObjectId,
  name: String (required),
  category: String (required, enum),
  coordinates: {
    lat: Number (required),
    lng: Number (required)
  },
  address: String,
  description: String,
  rating: Number (0-5),
  imageUrl: String,
  createdAt: Date,
  updatedAt: Date
}
```

## 🛠️ Environment Variables

```env
# Database
MONGODB_URI=mongodb://localhost:27017/gis_database
# Untuk MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/gis_database

# Server
PORT=3001

# Untuk CORS (optional)
# ALLOWED_ORIGINS=http://localhost:3000,https://yourdomain.com
```

## 🚀 Deploy ke Vercel

### 1. Push ke GitHub

```bash
git add .
git commit -m "Initial backend setup"
git push origin main
```

### 2. Buka Vercel

```
1. https://vercel.com
2. New Project > Import Repository
3. Pilih Backend-Geographic-Information-System
4. Add Environment Variables:
   - MONGODB_URI: mongodb+srv://...
   - PORT: 3001
5. Deploy
```

### 3. Update Frontend Config

Di aplikasi frontend, update `config.js`:

```javascript
const API_CONFIG = {
    BASE_URL: 'https://your-vercel-backend-url.vercel.app/api'
};
```

## 📊 MongoDB Atlas Setup

1. Daftar di https://www.mongodb.com/cloud/atlas
2. Buat Free Cluster
3. Dapatkan connection string
4. Whitelist IP: 0.0.0.0/0 (untuk Vercel)
5. Copy string ke `.env` -> `MONGODB_URI`

## 🐛 Troubleshooting

### MongoDB Connection Error
- Pastikan MongoDB service berjalan
- Check connection string di `.env`
- Whitelist IP di MongoDB Atlas (untuk cloud)

### CORS Error
- CORS sudah enabled di `server/index.js`
- Pastikan frontend origin sesuai

### Port Already in Use
```bash
# Windows
netstat -ano | findstr :3001
taskkill /PID <PID> /F

# Linux/Mac
lsof -i :3001
kill -9 <PID>
```

## 📝 Categories

- `restaurant` - Restoran
- `hotel` - Hotel
- `tourist_spot` - Tempat Wisata
- `school` - Sekolah
- `hospital` - Rumah Sakit
- `shop` - Toko
- `other` - Lainnya

## 🔗 Frontend Repository

Frontend aplikasi GIS tersedia di:
https://github.com/violasptntels/Geographic-Information-System

## 📄 License

MIT License

## 🙏 Credits

- Express.js
- MongoDB & Mongoose
- CORS

---

**Happy Coding! 🚀**
