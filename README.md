# AP EAMCET College Predictor 

A comprehensive web application that helps students predict their college admissions based on their EAMCET rank, category, and gender.

## 🚀 Features
- **🎯 Smart Predictions**: Accurate college predictions based on historical cutoff data
- **📊 Interactive Dashboard**: Visual representation of college data and trends
- **🔍 Advanced Search**: Filter colleges by name, location, branch, and more
- **⚖️ College Comparison**: Compare up to 5 colleges side by side
- **📱 Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices
- **🔐 Secure Authentication**: JWT-based user authentication and authorization
- **🌓 Dark/Light Mode**: Toggle between themes for comfortable viewing
- **❤️ Favorites System**: Save and manage your preferred colleges

  
## 🛠️ Tech Stack
| Category       | Technologies Used                          |
|----------------|-------------------------------------------|
| **Frontend**   | React, TypeScript, Vite, Tailwind CSS     |
| **Backend**    | Node.js, Express.js                       |
| **Database**   | MongoDB (with Mongoose ODM)               |
| **Auth**       | JWT, Bcrypt                              |


## 📋 Prerequisites

- Node.js (v16 or higher)
- MongoDB Atlas account
- npm or yarn package manager

## 🛠️ Installation

1. **Clone and setup**:
   ```bash
   cd backend
   npm install
   ```

2. **Environment Configuration**:
   ```bash
   cp .env.example .env
   ```
   
   Update `.env` with your configuration:
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/eamcet_predictor
   JWT_SECRET=your_super_secret_jwt_key_here
   PORT=5000
   NODE_ENV=development
   CORS_ORIGINS=http://localhost:3000,http://localhost:5173
   ```

3. **Start the server**:
   ```bash
   # Development
   npm run dev
   
   # Production
   npm start
   ```

## 📚 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Authentication Endpoints

#### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "role": "student"
}
```

#### Login User
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

#### Get Current User
```http
GET /api/auth/me
Authorization: Bearer <token>
```

### College Endpoints

#### Get College Predictions
```http
GET /api/colleges/predict?rank=5000&gender=BOYS&category=OC&branches=CSE,ECE&district=HYD&limit=50
```

#### Get All Colleges
```http
GET /api/colleges?page=1&limit=20&search=engineering&branch=CSE&type=GOVT
```

#### Get College Statistics
```http
GET /api/colleges/stats
```

#### Add New College (Admin Only)
```http
POST /api/colleges
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "INSTCODE": "TEST",
  "COLLEGE_NAME": "TEST ENGINEERING COLLEGE",
  "TYPE": "PVT",
  "REGION": "HYD",
  "DIST": "HYD",
  "PLACE": "HYDERABAD",
  "COED": "COED",
  "AFFL": "JNTUH",
  "ESTD": 2020,
  "branch_code": "CSE",
  "OC_BOYS": 10000,
  "OC_GIRLS": 12000,
  "COLLEGE_FEE": 150000
}
```

#### Upload CSV (Admin Only)
```http
POST /api/colleges/upload-csv
Authorization: Bearer <admin_token>
Content-Type: multipart/form-data

csvFile: <file>
```

### User Endpoints

#### Get Favorites
```http
GET /api/users/favorites
Authorization: Bearer <token>
```

#### Add to Favorites
```http
POST /api/users/favorites/:collegeId
Authorization: Bearer <token>
```

#### Remove from Favorites
```http
DELETE /api/users/favorites/:collegeId
Authorization: Bearer <token>
```

## 🗄️ Database Schema

### College Model
```javascript
{
  SNO: Number,
  INSTCODE: String,
  COLLEGE_NAME: String,
  TYPE: String, // GOVT, PVT, AIDED
  REGION: String,
  DIST: String,
  PLACE: String,
  COED: String, // COED, BOYS, GIRLS
  AFFL: String,
  ESTD: Number,
  branch_code: String,
  OC_BOYS: Number,
  OC_GIRLS: Number,
  // ... other cutoff fields
  COLLEGE_FEE: Number,
  year: Number,
  isActive: Boolean,
  timestamps: true
}
```

### User Model
```javascript
{
  name: String,
  email: String,
  password: String, // hashed
  role: String, // student, admin
  favorites: [ObjectId],
  profile: {
    rank: Number,
    category: String,
    gender: String,
    district: String
  },
  isActive: Boolean,
  lastLogin: Date,
  timestamps: true
}
```

## 🔒 Security Features

- **JWT Authentication**: Secure token-based authentication
- **Password Hashing**: bcrypt with salt rounds
- **Rate Limiting**: Prevents API abuse
- **Input Validation**: Comprehensive request validation
- **CORS Protection**: Configurable cross-origin requests
- **Helmet**: Security headers middleware
- **Role-based Access**: Admin-only endpoints protection

## 📊 Performance Optimizations

- **Database Indexing**: Optimized queries for predictions
- **Pagination**: Efficient data loading
- **Caching**: Ready for Redis integration
- **Batch Processing**: Efficient CSV uploads
- **Connection Pooling**: MongoDB connection optimization

## 🧪 Testing

```bash
# Run tests
npm test

# Run with coverage
npm run test:coverage
```

## 🚀 Deployment

### Environment Variables for Production
```env
NODE_ENV=production
MONGODB_URI=<production_mongodb_uri>
JWT_SECRET=<strong_production_secret>
PORT=5000
CORS_ORIGINS=https://yourdomain.com
```

### Deployment Platforms
- **Render**: Easy deployment with automatic builds
- **Heroku**: Classic PaaS platform
- **Railway**: Modern deployment platform
- **DigitalOcean App Platform**: Scalable hosting

## 📝 CSV Upload Format

The CSV file should contain the following columns:
```csv
SNO,INSTCODE,COLLEGE_NAME,TYPE,REGION,DIST,PLACE,COED,AFFL,ESTD,branch_code,OC_BOYS,OC_GIRLS,SC_BOYS,SC_GIRLS,ST_BOYS,ST_GIRLS,BCA_BOYS,BCA_GIRLS,BCB_BOYS,BCB_GIRLS,BCC_BOYS,BCC_GIRLS,BCD_BOYS,BCD_GIRLS,BCE_BOYS,BCE_GIRLS,OC_EWS_BOYS,OC_EWS_GIRLS,COLLEGE_FEE
```
## Output Screenshots
<img width="1904" height="1062" alt="image" src="https://github.com/user-attachments/assets/7f02fbdd-5620-41b0-b280-96d0fcdbdec3" />
<img width="1832" height="968" alt="image" src="https://github.com/user-attachments/assets/bc5fa634-8e2b-4bbb-9148-858e928edc51" />
<img width="1822" height="1060" alt="image" src="https://github.com/user-attachments/assets/b62aaf60-f7a4-46f1-bb7a-e945836398b6" />
<img width="1624" height="937" alt="image" src="https://github.com/user-attachments/assets/b38ccc79-16c0-4199-b687-f873a5fa6fe5" />
<img width="1780" height="1019" alt="image" src="https://github.com/user-attachments/assets/4a5e089d-1eca-4c34-b555-9a26e450b7c8" />


## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.
