# Node.js User Management Boilerplate

A production-ready Node.js boilerplate for user management with JWT authentication, role-based access control (RBAC), and MongoDB integration. This starter kit provides a solid foundation for building secure authentication systems.

## 🚀 Features

- ✅ **User Registration & Login** - Complete authentication flow
- ✅ **JWT Authentication** - Secure token-based authentication
- ✅ **Password Hashing** - bcrypt encryption for password security
- ✅ **Role-Based Access Control (RBAC)** - Admin and Customer roles
- ✅ **MongoDB Integration** - Mongoose ODM for database operations
- ✅ **Express.js REST API** - Clean and organized API structure
- ✅ **Environment Configuration** - Secure credential management
- ✅ **Input Validation** - Data validation and sanitization
- ✅ **Error Handling** - Comprehensive error handling

## 📋 Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB
- **ODM:** Mongoose
- **Authentication:** JWT (jsonwebtoken)
- **Password Encryption:** bcrypt
- **Environment Variables:** dotenv
- **Development:** nodemon

## 📁 Project Structure

```
Backend - User Management/
├── controllers/
│   └── userController.js      # User business logic
├── models/
│   └── user.js                # User schema/model
├── routes/
│   └── userRouter.js          # API route definitions
├── node_modules/              # Dependencies (not in git)
├── .env                       # Environment variables (not in git)
├── .env.example               # Environment template
├── .gitignore                 # Git ignore rules
├── index.js                   # Application entry point
├── package.json               # Project dependencies
└── README.md                  # Project documentation
```

## 🛠️ Installation

### Prerequisites

- Node.js (v14 or higher)
- MongoDB Atlas account or local MongoDB installation
- npm or yarn package manager

### Step 1: Clone the Repository

```bash
git clone https://github.com/nisal-G/nodejs-user-management_boilerplate.git
cd nodejs-user-management-boilerplate
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install:
- `express` - Web framework
- `mongoose` - MongoDB object modeling
- `bcrypt` - Password hashing
- `jsonwebtoken` - JWT authentication
- `dotenv` - Environment variable management
- `body-parser` - Request body parsing
- `nodemon` - Development auto-restart

### Step 3: Configure Environment Variables

Create a `.env` file in the root directory:

```bash
cp .env.example .env
```

Update the `.env` file with your credentials:

```env
MONGO_URL=mongodb+srv://username:password@cluster0.xxxxxx.mongodb.net/?appName=Cluster0
JWT_SECRET=your_secure_jwt_secret_key_here
```

**Generate a secure JWT secret:**
```bash
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

### Step 4: Setup MongoDB

1. Create a free account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster
3. Create a database user
4. Whitelist your IP address
5. Get your connection string and update `MONGO_URL` in `.env`

### Step 5: Start the Server

**Development mode (with auto-restart):**
```bash
npm start
```

**Production mode:**
```bash
node index.js
```

Server will run on `http://localhost:3000`

## 📚 API Documentation

### Base URL
```
http://localhost:3000/api
```

### Authentication

All protected routes require a JWT token in the Authorization header:
```
Authorization: Bearer <your_jwt_token>
```

---

### 1. User Registration

**Endpoint:** `POST /api/users`

**Description:** Register a new user

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "SecurePassword123!",
  "firstName": "John",
  "lastName": "Doe",
  "phone": "+1234567890",
  "role": "Customer",
  "whatsApp": "+1234567890",
  "disabled": false
}
```

**Response (Success - 200):**
```json
{
  "message": "User registered successfully"
}
```

**Response (Error - 500):**
```json
{
  "message": "User registration failed",
  "error": "Error details"
}
```

**Field Descriptions:**
- `email` (required) - User's email address (unique)
- `password` (required) - User's password (will be hashed)
- `firstName` (required) - User's first name
- `lastName` (required) - User's last name
- `phone` (optional) - Contact number
- `role` (optional) - User role: "Admin" or "Customer" (default: "Customer")
- `whatsApp` (optional) - WhatsApp number
- `disabled` (optional) - Account status (default: false)

---

### 2. User Login

**Endpoint:** `POST /api/users/logging`

**Description:** Authenticate user and receive JWT token

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "SecurePassword123!"
}
```

**Response (Success - 200):**
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

**Response (User Not Found - 404):**
```json
{
  "message": "User not found"
}
```

**Response (Invalid Password - 403):**
```json
{
  "message": "Invalid password"
}
```

---

## 🔐 Security Features

### Password Security
- Passwords are hashed using **bcrypt** with salt rounds of 10
- Original passwords are never stored in the database
- Password comparison is done securely using bcrypt.compare()

### JWT Authentication
- Tokens are signed with a secret key from environment variables
- Tokens contain user email and role information
- No expiration set by default (add expiration for production)

### Environment Variables
- Sensitive credentials stored in `.env` file
- `.env` file is gitignored to prevent exposure
- `.env.example` provided as a template

### Role-Based Access Control (RBAC)
- Two roles supported: **Admin** and **Customer**
- Helper functions to verify user roles:
  - `isItAdmin(req)` - Check if user is admin
  - `isItCustomer(req)` - Check if user is customer

## 🗄️ Database Schema

### User Model

```javascript
{
  email: {
    type: String,
    required: true,
    unique: true
  },
  password: {
    type: String,
    required: true
  },
  firstName: {
    type: String,
    required: true
  },
  lastName: {
    type: String,
    required: true
  },
  phone: {
    type: String,
    required: false
  },
  role: {
    type: String,
    required: true,
    default: "Customer"
  },
  whatsApp: {
    type: String,
    required: false
  },
  disabled: {
    type: Boolean,
    required: true,
    default: false
  }
}
```

## 🧪 Testing with Postman/Thunder Client

### Register a New User

```http
POST http://localhost:3000/api/users
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "Test123!",
  "firstName": "Test",
  "lastName": "User",
  "role": "Customer"
}
```

### Login

```http
POST http://localhost:3000/api/users/logging
Content-Type: application/json

{
  "email": "test@example.com",
  "password": "Test123!"
}
```

### Use JWT Token for Protected Routes

```http
GET http://localhost:3000/api/protected-route
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

## 🚧 Development

### Running in Development Mode

The project uses **nodemon** for automatic server restart on file changes:

```bash
npm start
```

### Code Structure

**index.js** - Main application file
- Express app initialization
- Middleware setup (body-parser, Authorization header handling)
- MongoDB connection
- Route mounting
- Server startup

**controllers/userController.js** - Business logic
- `registerUser()` - Handle user registration
- `loggingUser()` - Handle user login
- `isItAdmin()` - Check admin role
- `isItCustomer()` - Check customer role

**models/user.js** - Database schema
- Defines user data structure
- Mongoose schema and model

**routes/userRouter.js** - API routes
- Route definitions
- Controller mapping

## 📝 Environment Variables Reference

| Variable | Description | Required | Example |
|----------|-------------|----------|---------|
| `MONGO_URL` | MongoDB connection string | Yes | `mongodb+srv://user:pass@cluster.mongodb.net/` |
| `JWT_SECRET` | Secret key for JWT signing | Yes | `8ef8ff93181dc4e949f140d39047428a...` |
| `PORT` | Server port number | No | `3000` |
| `NODE_ENV` | Environment mode | No | `development` or `production` |

## 🔧 Customization

### Adding New Routes

1. Create controller function in `controllers/userController.js`
2. Add route in `routes/userRouter.js`
3. Import and use in `index.js`

Example:
```javascript
// controllers/userController.js
export function getUserProfile(req, res) {
  // Your logic here
}

// routes/userRouter.js
userRouter.get("/profile", getUserProfile);
```

### Adding Middleware

Edit `index.js` to add custom middleware:

```javascript
app.use((req, res, next) => {
  // Your middleware logic
  next();
});
```

### Modifying User Schema

Edit `models/user.js` to add/remove fields:

```javascript
const userSchema = mongoose.Schema({
  // Add new fields here
  address: {
    type: String,
    required: false
  }
});
```

## ⚠️ Important Security Notes

### Before Production:

1. **Add JWT Expiration:**
```javascript
const token = jwt.sign(payload, process.env.JWT_SECRET, { expiresIn: '24h' });
```

2. **Add Rate Limiting:**
```bash
npm install express-rate-limit
```

3. **Add Helmet for Security Headers:**
```bash
npm install helmet
```

4. **Add CORS Configuration:**
```bash
npm install cors
```

5. **Add Input Validation:**
```bash
npm install joi
```

6. **Enable HTTPS** in production

7. **Use Strong JWT Secrets** (minimum 32 characters)

8. **Implement Password Requirements** (min length, complexity)

9. **Add Email Verification** for new registrations

10. **Implement Refresh Tokens** for better security

## 🐛 Common Issues & Solutions

### MongoDB Connection Failed
- Check internet connection
- Verify MongoDB Atlas IP whitelist
- Confirm credentials in `.env`
- Check cluster status on MongoDB Atlas

### JWT Token Invalid
- Ensure token is sent with "Bearer " prefix
- Check JWT_SECRET matches in `.env`
- Verify token hasn't expired (if expiration is set)

### Port Already in Use
```bash
# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Change port in .env
PORT=3001
```

### bcrypt Installation Error
```bash
npm rebuild bcrypt --build-from-source
```

## 📦 Dependencies

```json
{
  "bcrypt": "^5.1.1",           // Password hashing
  "body-parser": "^1.20.3",     // Parse request bodies
  "dotenv": "^16.4.7",          // Environment variables
  "express": "^4.21.2",         // Web framework
  "jsonwebtoken": "^9.0.2",     // JWT authentication
  "mongoose": "^8.9.5",         // MongoDB ODM
  "nodemon": "^3.1.9"           // Development tool
}
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

Your Name
- GitHub: [@yourusername](https://github.com/yourusername)
- Email: your.email@example.com

## 🙏 Acknowledgments

- Express.js team for the amazing framework
- MongoDB team for the database
- JWT.io for authentication standards
- bcrypt for secure password hashing

## 📞 Support

For support, email your.email@example.com or create an issue in the repository.

---

**Made with ❤️ using Node.js and Express**
