# Angular Todo Application

## Project Overview

This is a full-stack Angular Todo Application with a Node.js/Express backend and MongoDB database. The application allows users to create, manage, and organize tasks with different priorities and statuses.

### Key Features
- **User Authentication**: Email/password login and registration
- **Demo Mode**: Quick testing without creating an account
- **Task Management**: Create, edit, delete, and filter todos
- **Priority Levels**: Organize tasks by priority (low, medium, high)
- **Status Tracking**: Track task status (pending, in-progress, completed)
- **Responsive Design**: Works on desktop and mobile devices
- **Secure**: JWT-based authentication with password hashing

---

## Architecture Overview

### Frontend (Angular)
Located in: `/frontend`

**Key Components:**
1. **AuthShell** - Container for login/register pages
2. **Login** - User authentication form with demo mode
3. **Register** - New user account creation
4. **TodoApp** - Main application with task management
5. **Services** - Authentication and todo data management

### Backend (Node.js/Express)
Located in: `/backend`

**Key Components:**
1. **Controllers** - Request handlers for auth and todos
2. **Models** - MongoDB schemas (User, Todo)
3. **Routes** - API endpoints
4. **Middleware** - Authentication and request processing
5. **Utils** - JWT token generation
6. **Config** - Database connection setup

---

## Frontend Architecture

### Directory Structure
```
frontend/src/
├── app/
│   ├── components/
│   │   ├── auth-shell/      # Authentication layout container
│   │   ├── login/           # Login component
│   │   ├── register/        # Registration component
│   │   └── todo-app/        # Main todo component
│   ├── core/
│   │   ├── guards/          # Route guards (auth.guard.ts)
│   │   ├── interceptors/    # HTTP interceptors (auth.interceptor.ts)
│   │   └── services/        # Application services
│   ├── models/              # TypeScript interfaces (todo.model.ts)
│   ├── pipes/               # Custom pipes for formatting
│   ├── app.config.ts        # Angular app configuration
│   ├── app.routes.ts        # Route definitions
│   └── app.ts               # Root component
├── main.ts                  # Application entry point
└── index.html               # HTML template
```

### Core Services

#### AuthService (`src/app/core/services/auth.service.ts`)
**Purpose**: Manages user authentication and session state

**Key Methods:**
- `login(email, password)` - Authenticates user with credentials
- `demoLogin()` - Creates temporary demo account
- `setSession(data)` - Saves token and user info
- `logout()` - Clears authentication
- `setToken(token, user)` - Sets token and user manually

**State Management:**
- `token` Signal - Current JWT token
- `user` Signal - Current user object
- `isLoggedIn` Computed - Whether user is authenticated
- `isDemo` Computed - Whether user is using demo mode

#### TodoService (`src/app/core/services/todo.service.ts`)
**Purpose**: Handles all todo CRUD operations

**Key Methods:**
- `loadTodos()` - Fetches user's todos from backend
- `createTodo(todo)` - Creates new todo
- `updateTodo(id, updates)` - Updates existing todo
- `deleteTodo(id)` - Deletes todo

**Enums:**
- `Priority`: 1=low, 2=medium, 3=high
- `Status`: 1=pending, 2=in-progress, 3=completed

**State Management:**
- `todos` Signal - Current list of todos

### Component Details

#### Login Component
**Features:**
- Email/password authentication
- Demo login option
- Error handling with user-friendly messages
- Form validation

**Methods:**
- `login()` - Authenticates with email/password
- `loginDemo()` - Authenticates as demo user
- `goRegister()` - Navigates to registration

#### Register Component
**Features:**
- New account creation
- Password confirmation matching
- Email validation
- Error handling for duplicate emails

**Methods:**
- `register()` - Creates new user account

#### TodoApp Component
**Features:**
- Create, read, update, delete todos
- Filter todos by status and priority
- Sort todos
- Search/filter functionality
- Edit inline or modal
- Toggle task completion

**Key Computed Properties:**
- `filteredList` - Todos filtered by search term
- `sortedList` - Sorted filtered todos
- `totalTasks` - Count of all tasks
- `pendingTasks` - Count of pending tasks
- `inProgressTasks` - Count of in-progress tasks
- `completedTasks` - Count of completed tasks

**Key Methods:**
- `onSaveNewTask()` - Creates new todo
- `onCheckTask(taskId)` - Toggles task status
- `onEditTask(taskId)` - Prepares task for editing
- `onSaveEdit()` - Saves edited task
- `onCancelEdit()` - Cancels edit operation
- `onDeleteTask(taskId)` - Deletes todo
- `logout()` - Logs out user

---

## Backend Architecture

### Directory Structure
```
backend/src/
├── controllers/
│   ├── auth.controller.js       # Authentication endpoints
│   └── todo.controller.js       # Todo CRUD endpoints
├── models/
│   ├── User.js                  # User schema
│   └── Todo.js                  # Todo schema
├── routes/
│   ├── auth.routes.js           # Auth endpoints routing
│   └── todo.routes.js           # Todo endpoints routing
├── middleware/
│   ├── auth.middleware.js       # JWT verification
│   └── demoGuard.middleware.js  # Demo user flag
├── config/
│   └── db.js                    # MongoDB connection
├── utils/
│   └── jwt.js                   # JWT token generation
├── seed/
│   ├── demoUser.js              # Demo user setup
│   └── resetDemoTodos.js        # Reset demo todos
├── app.js                       # Express app setup
└── server.js                    # Server entry point
```

### Database Models

#### User Model
```javascript
{
  email: String (unique, lowercase)
  password: String (hashed)
  role: String (recruiter|candidate|demo)
  isDemo: Boolean
  createdAt: Date
  updatedAt: Date
}
```

#### Todo Model
```javascript
{
  todoItem: String (required)
  createDate: Date
  priority: Number (0|1|2|3)
  status: Number (0|1|2|3)
  isNew: Boolean
  user: ObjectId (ref: User)
  createdAt: Date
  updatedAt: Date
}
```

### API Endpoints

#### Authentication Endpoints

**POST /auth/login**
- Request: `{ email, password }`
- Response: `{ token, user: { id, email, role, isDemo } }`
- Description: Authenticates user with credentials

**POST /auth/register**
- Request: `{ email, password }`
- Response: `{ token, user: { id, email } }`
- Description: Creates new user account

**POST /auth/demo**
- Request: `{}`
- Response: `{ token, user: { id, email, role, isDemo } }`
- Description: Creates temporary demo user with sample todos

#### Todo Endpoints (All require authentication)

**GET /todos**
- Response: `[{ _id, todoItem, createDate, priority, status, user }]`
- Description: Retrieves all todos for authenticated user

**POST /todos**
- Request: `{ todoItem, priority, status, createDate }`
- Response: `{ _id, todoItem, createDate, priority, status, user }`
- Description: Creates new todo

**PUT /todos/:id**
- Request: `{ todoItem?, priority?, status?, createDate? }`
- Response: `{ _id, todoItem, createDate, priority, status, user }`
- Description: Updates existing todo

**DELETE /todos/:id**
- Response: `{ message: "Todo deleted" }`
- Description: Deletes todo

### Middleware

#### Auth Middleware (`auth.middleware.js`)
**Purpose**: Verifies JWT token from Authorization header
- Extracts token from "Bearer <token>" format
- Validates token signature
- Attaches decoded user data to request

#### Demo Guard Middleware (`demoGuard.middleware.js`)
**Purpose**: Flags demo user requests
- Sets `req.isDemo` if user is demo account
- Allows downstream handlers to apply demo-specific logic

### Controllers

#### Auth Controller (`auth.controller.js`)
- `login()` - Authenticates user, returns token
- `register()` - Creates new account, returns token
- `demoLogin()` - Creates demo account with sample todos

#### Todo Controller (`todo.controller.js`)
- `createTodo()` - Creates new todo with user ID
- `getTodos()` - Retrieves user's todos
- `updateTodo()` - Updates todo (with user verification)
- `deleteTodo()` - Deletes todo (with user verification)

---

## Security Features

1. **Authentication**: JWT-based token authentication
2. **Password Security**: Bcrypt hashing with salt rounds
3. **Authorization**: User can only access their own todos
4. **CORS**: Configured for specific origins
5. **Security Headers**: Helmet.js CSP (Content Security Policy)
6. **Input Validation**: Basic required field validation
7. **Error Handling**: Generic error messages to prevent information leakage

---

## Data Flow

### User Login Flow
1. User enters email/password in Login component
2. AuthService.login() sends credentials to backend
3. Backend verifies credentials, generates JWT token
4. Token stored in signal and localStorage
5. Auth interceptor attaches token to subsequent requests
6. User navigated to Todo app

### Create Todo Flow
1. User enters todo details in TodoApp component
2. onSaveNewTask() validates input
3. TodoService.createTodo() sends to backend with auth token
4. Backend verifies token, creates todo with user ID
5. Todo optimistically added to local signal
6. Backend response updates signal with full data

### Update Todo Flow
1. User edits todo in TodoApp component
2. onSaveEdit() validates changes
3. TodoService.updateTodo() sends to backend
4. Backend verifies ownership, updates todo
5. Local signal updated with new values

---

## Development Workflow

### Frontend Development
```bash
cd todoApp
npm install
ng serve
# App runs at http://localhost:4200
```

### Backend Development
```bash
cd todo-backend
npm install
npm start
# Server runs at http://localhost:5000
```

### Key Npm Scripts

**Frontend:**
- `ng serve` - Start dev server
- `ng build` - Production build
- `ng test` - Run tests
- `ng lint` - Run linter

**Backend:**
- `npm start` - Start server
- `nodemon` - Dev server with auto-reload

---

## Environment Variables

### Frontend (.env or environment files)
- API_URL - Backend API base URL

### Backend (.env)
- `MONGO_URI` - MongoDB connection string
- `JWT_SECRET` - Secret for JWT signing
- `JWT_EXPIRES_IN` - Token expiration (e.g., "7d")
- `PORT` - Server port (default: 5000)
- `NODE_ENV` - Environment (development/production)

---

## Best Practices Implemented

### Frontend
- Standalone components (modern Angular)
- Signals for reactive state
- Computed properties for derived state
- Proper error handling
- HTTP interceptors for auth tokens
- Route guards for protected routes
- Responsive CSS layout
- Form validation
- Comprehensive JSDoc comments

### Backend
- RESTful API design
- Proper HTTP status codes
- Error handling middleware
- Security headers (Helmet)
- CORS configuration
- Environment variable management
- Password hashing with bcrypt
- JWT token authentication
- User data isolation (queries filtered by user)
- Comprehensive JSDoc comments

---

## Testing Recommendations

### Frontend Tests
- Component initialization and rendering
- User authentication flows
- Todo CRUD operations
- Filter and sort functionality
- Error handling and display
- Signal updates and computed properties

### Backend Tests
- Authentication endpoints
- Todo CRUD endpoints
- Authorization (user isolation)
- Error responses
- Database operations
- Token verification

---

## Deployment

### Frontend Deployment
Built Angular app can be deployed to:
- Netlify
- Vercel
- GitHub Pages
- AWS S3 + CloudFront
- Azure Static Web Apps

### Backend Deployment
Backend can be deployed to:
- Heroku
- AWS EC2/Lambda
- DigitalOcean
- Railway
- Render.com
- Azure App Service

---

## Troubleshooting

### Common Issues

**CORS Error**
- Ensure backend CORS is configured correctly
- Check that credentials are sent if needed

**Token Expired**
- Implement token refresh mechanism
- Or guide user to login again

**MongoDB Connection Failed**
- Verify MONGO_URI is correct
- Check network access in MongoDB Atlas
- Ensure database user has correct permissions

**Todos Not Loading**
- Verify JWT token is valid
- Check user authentication status
- Verify backend is running

---

## Performance Optimization

### Frontend
- Use OnPush change detection strategy
- Lazy load routes
- Implement virtual scrolling for large lists
- Cache HTTP responses
- Minimize bundle size

### Backend
- Add database indexes on frequently queried fields
- Implement pagination for large result sets
- Add response caching headers
- Use compression middleware
- Monitor and optimize database queries

---

## Future Enhancements

1. **Features**
   - Task categories/tags
   - Recurring tasks
   - Task reminders/notifications
   - Collaboration (share tasks)
   - Dark mode

2. **Technical**
   - Unit and integration tests
   - E2E tests
   - API documentation (Swagger/OpenAPI)
   - Database migrations
   - Logging and monitoring
   - Rate limiting
   - Request validation (joi/yup)

3. **Performance**
   - GraphQL API
   - Real-time updates (WebSocket)
   - Offline support (Service Workers)
   - Database query optimization

---

## Code Style and Conventions

### Naming
- Components: PascalCase (e.g., `TodoApp`)
- Services: PascalCase (e.g., `AuthService`)
- Files: kebab-case (e.g., `auth.service.ts`)
- Variables/functions: camelCase
- Constants: UPPER_SNAKE_CASE

### Comments
- JSDoc style for functions and classes
- Inline comments for complex logic
- Clear, descriptive comment text

### Structure
- One component per file
- Services in separate files
- Interfaces/types at top of file
- Imports organized by category

---

## Additional Resources

- [Angular Documentation](https://angular.io)
- [Express.js Guide](https://expressjs.com)
- [MongoDB Manual](https://docs.mongodb.com/manual)
- [JWT Introduction](https://jwt.io/introduction)
- [REST API Best Practices](https://restfulapi.net)
