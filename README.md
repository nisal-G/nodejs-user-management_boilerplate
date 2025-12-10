Node.js User Management Boilerplate

A clean and production-ready Node.js boilerplate for user authentication using JWT, MongoDB, and role-based access control.

🚀 Features

User Registration & Login

JWT Authentication

Password Hashing (bcrypt)

Role-Based Access Control (Admin / Customer)

MongoDB + Mongoose

Express.js REST API

Organized MVC structure

Environment variables support

Error handling

📦 Tech Stack

Node.js, Express.js

MongoDB, Mongoose

JWT, bcrypt

dotenv, nodemon

📁 Folder Structure
Backend - User Management/
├── controllers/
├── models/
├── routes/
├── index.js
├── package.json
├── .env.example
└── README.md

🛠️ Installation
1️⃣ Clone the Repo
git clone https://github.com/nisal-G/nodejs-user-management_boilerplate.git
cd nodejs-user-management-boilerplate

2️⃣ Install Dependencies
npm install

3️⃣ Setup Environment Variables

Create .env:

cp .env.example .env


Add:

MONGO_URL=your_mongodb_connection
JWT_SECRET=your_secret_key
PORT=3000


Generate a secret key:

node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"

▶️ Run the Project
Development:
npm start

Production:
node index.js


Server runs at:

http://localhost:3000

📚 API Endpoints
👉 Register User

POST /api/users

{
  "email": "user@example.com",
  "password": "Password123",
  "firstName": "John",
  "lastName": "Doe"
}

👉 Login

POST /api/users/logging

{
  "email": "user@example.com",
  "password": "Password123"
}

Protected Routes

Use token:

Authorization: Bearer <token_here>

🗄️ User Schema (Simple Overview)
{
  email: String,
  password: String,
  firstName: String,
  lastName: String,
  role: { type: String, default: "Customer" },
  disabled: { type: Boolean, default: false }
}

🔧 Customize

Add new endpoints → controllers/ + routes/

Add fields → models/user.js

Add middleware → index.js

🤝 Contributing

Fork

Create branch

Commit

Push

Open PR

📄 License

MIT License.

👨‍💻 Author

Nisal Gunathilaka
GitHub: https://github.com/nisal-G
