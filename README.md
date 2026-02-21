# Angular Todo App 

A full-stack todo application showcasing modern web development with Angular, Node.js, and MongoDB.

## Live Demo

**Frontend**: [Live App](https://zas-angulartodoapp.netlify.app/) \
**Backend API**: Deployed on Fly.io 

## Features

- User authentication with JWT
- Demo mode to test instantly
- Full CRUD operations for todos
- Filter by status (pending, in-progress, completed)
- Priority levels (low, medium, high)
- Search functionality
- Responsive design
- Comprehensive error handling

## Tech Stack

### Frontend
- Angular 21

### Backend
- Node.js & Express
- MongoDB with Mongoose
- JWT authentication
- Bcrypt password hashing
- Helmet security middleware

## Running Locally

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


## Project Structure

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

## Security Features

- JWT-based authentication
- Password hashing with bcrypt (10 rounds)
- Protected routes with auth middleware
- User data isolation (users only see their own todos)
- CORS configuration
- Helmet security headers
- Environment variable protection

## Documentation

See **PROJECT_DOCUMENTATION.md** for complete architecture details, API endpoints, and code examples.

