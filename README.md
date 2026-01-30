# Angular Todo App - Portfolio Project

A full-stack todo application showcasing modern web development with Angular, Node.js, and MongoDB.

## 🚀 Live Demo

**Frontend**: [Live App](https://zas-angulartodoapp.netlify.app/)

**Backend API**: Deployed on Render

## 📋 Features

- ✅ User authentication with JWT
- ✅ Demo mode for recruiters to test instantly
- ✅ Full CRUD operations for todos
- ✅ Filter by status (pending, in-progress, completed)
- ✅ Priority levels (low, medium, high)
- ✅ Search functionality
- ✅ Responsive design
- ✅ Comprehensive error handling

## 🛠️ Tech Stack

### Frontend
- Angular 17+ (Standalone Components)
- TypeScript
- Angular Signals for state management
- RxJS for async operations
- Reactive Forms

### Backend
- Node.js & Express
- MongoDB with Mongoose
- JWT authentication
- Bcrypt password hashing
- Helmet security middleware

## 📱 Running Locally

### Prerequisites
- Node.js 18+
- MongoDB connection string

### Frontend Setup
```bash
cd frontend
npm install
ng serve
# App runs at http://localhost:4200
```

### Backend Setup
```bash
cd backend
npm install

# Create .env file:
# MONGO_URI=your_mongodb_uri
# JWT_SECRET=your_secret_key
# JWT_EXPIRES_IN=7d
# PORT=5000

npm start
# API runs at http://localhost:5000
```

## 🎨 Code Quality

- **100% JSDoc Documentation**: All 16 code files fully documented
- **TypeScript**: Type-safe frontend code
- **Clean Architecture**: Separation of concerns with services, controllers, and models
- **Security**: JWT auth, password hashing, CORS, security headers
- **Professional Standards**: Follows Angular and Node.js best practices

## 📂 Project Structure

```
angular-todo-app/
├── frontend/             # Angular frontend
│   └── src/
│       ├── app/
│       │   ├── components/    # UI components
│       │   ├── core/
│       │   │   └── services/  # Business logic
│       │   └── models/        # TypeScript interfaces
│       └── environments/      # Dev/Prod configs
│
└── backend/              # Node.js backend
    └── src/
        ├── controllers/  # Route handlers
        ├── models/       # MongoDB schemas
        ├── routes/       # API endpoints
        ├── middleware/   # Auth & validation
        └── utils/        # Helper functions
```

## 🔐 Security Features

- JWT-based authentication
- Password hashing with bcrypt (10 rounds)
- Protected routes with auth middleware
- User data isolation (users only see their own todos)
- CORS configuration
- Helmet security headers
- Environment variable protection

## 📖 Documentation

See **PROJECT_DOCUMENTATION.md** for complete architecture details, API endpoints, and code examples.

## 👨‍💻 About

This project was built to demonstrate:
- Full-stack development skills
- Modern Angular patterns (Signals, Standalone Components)
- RESTful API design
- Authentication and authorization
- Database design and relationships
- Professional code documentation
- Clean, maintainable code

---

**Portfolio Project** | Built with Angular & Node.js
