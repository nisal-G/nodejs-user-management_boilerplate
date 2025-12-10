# Node.js User Management Boilerplate

A clean and production-ready Node.js boilerplate for user authentication using JWT, MongoDB, and role-based access control.

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)

## 🚀 Features

- ✅ **User Registration & Login** - Complete authentication flow
- ✅ **JWT Authentication** - Secure token-based authentication
- ✅ **Password Hashing** - bcrypt encryption for password security
- ✅ **Role-Based Access Control** - Admin and Customer roles
- ✅ **MongoDB + Mongoose** - Database integration
- ✅ **Express.js REST API** - Clean API structure
- ✅ **Organized MVC Structure** - Scalable code organization
- ✅ **Environment Variables** - Secure configuration
- ✅ **Error Handling** - Comprehensive error management

## 📦 Tech Stack

| Technology | Purpose |
|------------|---------|
| **Node.js** | Runtime environment |
| **Express.js** | Web framework |
| **MongoDB** | Database |
| **Mongoose** | ODM for MongoDB |
| **JWT** | Authentication tokens |
| **bcrypt** | Password hashing |
| **dotenv** | Environment variables |
| **nodemon** | Development auto-reload |

## 📁 Project Structure

```
Backend - User Management/
├── controllers/
│   └── userController.js    # Business logic
├── models/
│   └── user.js              # Database schema
├── routes/
│   └── userRouter.js        # API routes
├── index.js                 # Entry point
├── package.json             # Dependencies
├── .env.example             # Environment template
└── README.md                # Documentation
```

## 🛠️ Installation

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/nisal-G/nodejs-user-management_boilerplate.git
cd nodejs-user-management_boilerplate
```

### 2️⃣ Install Dependencies

```bash
npm install
```

### 3️⃣ Setup Environment Variables

Create a `.env` file:

```bash
cp .env.example .env
```

Add your configuration:

```env
MONGO_URL=your_mongodb_connection_string
JWT_SECRET=your_secret_key
```

**Generate a secure JWT secret:**

```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

### 4️⃣ Configure MongoDB

- Create a free account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- Create a cluster and database user
- Get your connection string
- Update `MONGO_URL` in `.env`

## ▶️ Run the Project

**Development mode (with auto-reload):**

```bash
npm start
```

**Production mode:**

```bash
node index.js
```

Server runs at: **http://localhost:3000**

## 📚 API Endpoints

### Base URL
```
http://localhost:3000/api
```

---

### 👉 Register User

**Endpoint:** `POST /api/users`

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "Password123",
  "firstName": "John",
  "lastName": "Doe"
}
```

**Response:**
```json
{
  "message": "User registered successfully"
}
```

---

### 👉 Login

**Endpoint:** `POST /api/users/logging`

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "Password123"
}
```

**Response:**
```json
{
  "message": "User logged in successfully",
  "user": {
    "email": "user@example.com",
    "firstName": "John",
    "lastName": "Doe",
    "role": "Customer"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

### 🔒 Protected Routes

Use the JWT token in the Authorization header:

```http
Authorization: Bearer <your_token_here>
```

## 🗄️ User Schema

```javascript
{
  email: String,          // Unique email address
  password: String,       // Hashed password
  firstName: String,      // User's first name
  lastName: String,       // User's last name
  phone: String,          // Optional phone number
  role: {
    type: String,
    default: "Customer"   // "Admin" or "Customer"
  },
  whatsApp: String,       // Optional WhatsApp number
  disabled: {
    type: Boolean,
    default: false        // Account status
  }
}
```

## 🔧 Customization

### Add New Endpoints

1. Create controller function in `controllers/userController.js`
2. Add route in `routes/userRouter.js`
3. Test with Postman/Thunder Client

### Add New Fields

Edit `models/user.js`:

```javascript
const userSchema = mongoose.Schema({
  // Add your new fields here
  address: {
    type: String,
    required: false
  }
});
```

### Add Middleware

Edit `index.js`:

```javascript
app.use((req, res, next) => {
  // Your custom middleware
  next();
});
```

## 🧪 Testing

### Using Postman/Thunder Client

**1. Register a user:**
```http
POST http://localhost:3000/api/users
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "Test123",
  "firstName": "Test",
  "lastName": "User"
}
```

**2. Login:**
```http
POST http://localhost:3000/api/users/logging
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "Test123"
}
```

**3. Copy the token and use it for protected routes**

## 🔐 Security Features

- **Password Hashing:** bcrypt with salt rounds of 10
- **JWT Tokens:** Signed with secret key from environment
- **Role-Based Access:** Admin and Customer roles
- **Environment Variables:** Sensitive data not in code
- **Gitignore:** `.env` file excluded from version control

## 📝 Environment Variables

| Variable | Description | Required | Example |
|----------|-------------|----------|---------|
| `MONGO_URL` | MongoDB connection string | Yes | `mongodb+srv://user:pass@cluster...` |
| `JWT_SECRET` | Secret key for JWT | Yes | `8ef8ff93181dc4e949f140...` |
| `PORT` | Server port | No | `3000` |

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork** the repository
2. **Create** your feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

## 📄 License

This project is licensed under the **MIT License**.

## 👨‍💻 Author

**Nisal Gunathilaka**

- GitHub: [@nisal-G](https://github.com/nisal-G)
- Repository: [nodejs-user-management-boilerplate](https://github.com/nisal-G/nodejs-user-management_boilerplate)

## 🙏 Acknowledgments

- Express.js team for the amazing framework
- MongoDB team for the database
- JWT.io for authentication standards
- The Node.js community

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!

---

**Built with ❤️ using Node.js and Express**
