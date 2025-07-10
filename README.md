# JSON Server Vercel Deployment Documentation

## Overview
Dokumentasi ini menjelaskan cara deploy JSON Server ke Vercel untuk membuat REST API sederhana yang dapat digunakan untuk testing dan development.

## Struktur Project
```
your-project/
├── api/
│   └── server.js
├── db.json
├── package.json
└── vercel.json
```

## Setup dan Deployment

### 1. Persiapan Project
Buat folder project baru dan struktur file sesuai dengan struktur di atas.

### 2. Konfigurasi package.json
```json
{
  "name": "json-server-vercel",
  "version": "1.0.0",
  "description": "Deploy JSON Server to Vercel",
  "main": "api/server.js",
  "scripts": {
    "start": "node api/server.js"
  },
  "dependencies": {
    "json-server": "^0.17.4"
  }
}
```

### 3. Upload ke GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/username/repository-name.git
git push -u origin main
```

### 4. Deploy ke Vercel
1. Buka [vercel.com](https://vercel.com)
2. Login dengan GitHub
3. Click "New Project"
4. Import repository Anda
5. Konfigurasi deployment:
   - **Build Command**: kosongkan atau `echo "No build needed"`
   - **Output Directory**: kosongkan
   - **Install Command**: `npm install`
6. Click "Deploy"

## API Endpoints

Setelah deployment berhasil, API akan tersedia di `https://your-project.vercel.app/`

### Available Endpoints:

#### Users
- `GET /user` - Mendapatkan semua user
- `GET /user/{id}` - Mendapatkan user berdasarkan ID
- `POST /user` - Membuat user baru
- `PUT /user/{id}` - Update user berdasarkan ID
- `DELETE /user/{id}` - Hapus user berdasarkan ID

#### Doctors
- `GET /doctors` - Mendapatkan semua doctor
- `GET /doctors/{id}` - Mendapatkan doctor berdasarkan ID
- `POST /doctors` - Membuat doctor baru
- `PUT /doctors/{id}` - Update doctor berdasarkan ID
- `DELETE /doctors/{id}` - Hapus doctor berdasarkan ID

#### Konsuls
- `GET /konsuls` - Mendapatkan semua konsultasi
- `GET /konsuls/{id}` - Mendapatkan konsultasi berdasarkan ID
- `POST /konsuls` - Membuat konsultasi baru
- `PUT /konsuls/{id}` - Update konsultasi berdasarkan ID
- `DELETE /konsuls/{id}` - Hapus konsultasi berdasarkan ID

## Contoh Penggunaan

### 1. Mendapatkan Semua User
```bash
curl https://your-project.vercel.app/user
```

### 2. Mendapatkan User Berdasarkan ID
```bash
curl https://your-project.vercel.app/user/1
```

### 3. Membuat User Baru
```bash
curl -X POST https://your-project.vercel.app/user \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "username": "johndoe",
    "password": "password123",
    "email": "john@example.com",
    "phone": "1234567890",
    "country": "Indonesia",
    "address": "Jakarta",
    "role": "user",
    "gender": "male"
  }'
```

### 4. Update User
```bash
curl -X PUT https://your-project.vercel.app/user/1 \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Updated Name",
    "email": "updated@example.com"
  }'
```

### 5. Hapus User
```bash
curl -X DELETE https://your-project.vercel.app/user/1
```

## Query Parameters

JSON Server mendukung berbagai query parameters untuk filtering dan sorting:

### Filtering
```bash
# Filter berdasarkan field
GET /user?role=admin
GET /doctors?name=Dr. Ahmad

# Filter multiple conditions
GET /user?role=admin&gender=female
```

### Sorting
```bash
# Sort ascending
GET /user?_sort=name&_order=asc

# Sort descending
GET /user?_sort=id&_order=desc
```

### Pagination
```bash
# Limit hasil
GET /user?_limit=5

# Pagination dengan page
GET /user?_page=1&_limit=10
```

### Search
```bash
# Search di semua field
GET /user?q=admin

# Search di field tertentu
GET /user?name_like=John
```

## Response Format

### Success Response
```json
{
  "id": 1,
  "name": "Nihira",
  "username": "adminuser",
  "email": "nihiratechiees@gmail.com",
  "role": "admin"
}
```

### Error Response
```json
{
  "error": "Not found"
}
```

## Testing dengan JavaScript

### Fetch API
```javascript
// GET request
fetch('https://your-project.vercel.app/user')
  .then(response => response.json())
  .then(data => console.log(data));

// POST request
fetch('https://your-project.vercel.app/user', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'New User',
    email: 'newuser@example.com'
  })
})
.then(response => response.json())
.then(data => console.log(data));
```

### Axios
```javascript
// GET request
axios.get('https://your-project.vercel.app/user')
  .then(response => console.log(response.data));

// POST request
axios.post('https://your-project.vercel.app/user', {
  name: 'New User',
  email: 'newuser@example.com'
})
.then(response => console.log(response.data));
```

## Important Notes

1. **Data Persistence**: Data akan reset setiap kali deployment baru. Untuk data persisten, gunakan database eksternal.

2. **CORS**: API sudah dikonfigurasi untuk menerima request dari domain manapun.

3. **Rate Limiting**: Vercel memiliki rate limiting untuk free tier.

4. **File Size**: Pastikan file `db.json` tidak terlalu besar (< 1MB recommended).

5. **Auto-deploy**: Setiap push ke GitHub akan otomatis trigger deployment baru.

## Troubleshooting

### 404 Not Found
- Pastikan struktur folder benar
- Cek konfigurasi `vercel.json`
- Pastikan file `db.json` ada di root directory

### 500 Internal Server Error
- Cek logs di Vercel dashboard
- Pastikan syntax JSON valid di `db.json`
- Cek dependencies di `package.json`

### CORS Issues
- API sudah dikonfigurasi untuk CORS
- Jika masih ada masalah, coba akses langsung dari browser terlebih dahulu

## Support
Untuk pertanyaan lebih lanjut, silakan check:
- [JSON Server Documentation](https://github.com/typicode/json-server)
- [Vercel Documentation](https://vercel.com/docs)
