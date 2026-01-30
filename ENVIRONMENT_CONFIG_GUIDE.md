# Environment Configuration Guide

Your Angular Todo App now supports switching between development and production environments!

## Files Created

### 1. `src/environments/environment.ts` - Development
```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:5000'  // Local backend
};
```

### 2. `src/environments/environment.prod.ts` - Production
```typescript
export const environment = {
  production: true,
  apiUrl: 'https://your-deployed-backend-url.com'  
};
```

## How to Use

### Development (Local)
```bash
# Run locally with dev environment
cd todoApp
ng serve

# Or explicitly with development config
ng serve --configuration development
```

**Uses**: `environment.ts` → Points to `http://localhost:5000` (your local backend)

### Production Build
```bash
# Build for production (uses environment.prod.ts)
ng build --configuration production

# Or the default:
ng build
```

**Uses**: `environment.prod.ts` → Points to your deployed backend URL

## Configuration Steps

### 1. Update Production URL
Edit `src/environments/environment.prod.ts`:

```typescript
export const environment = {
  production: true,
  apiUrl: 'https://your-actual-deployed-backend-url.com'  // ← Replace this
};
```

Replace `https://your-actual-deployed-backend-url.com` with:
- Your Render deployment: `https://your-app.onrender.com`
- Your AWS URL: `https://your-api.amazonaws.com`
- Or wherever your backend is deployed

### 2. Services Updated
Both services now import and use the environment config:

**auth.service.ts**:
```typescript
import { environment } from '../../../environments/environment';

export class AuthService {
  private readonly API = `${environment.apiUrl}/auth`;
  // ...
}
```

**todo.service.ts**:
```typescript
import { environment } from '../../../environments/environment';

export class TodoService {
  private readonly API = `${environment.apiUrl}/todos`;
  // ...
}
```

## Quick Commands

```bash
# Development - connects to localhost:5000
ng serve

# Production build - uses production environment
ng build

# Deploy production build
# (Upload the dist/ folder to your hosting provider)
```

## Adding More Environments

If you need additional environments (staging, etc.), follow this pattern:

1. Create `src/environments/environment.staging.ts`
2. Add config to `angular.json` under `build.configurations`
3. Use: `ng serve --configuration staging`

## Debugging

To verify which environment is being used:

```typescript
// In any component
import { environment } from './environments/environment';

ngOnInit() {
  console.log('Using environment:', environment.apiUrl);
  console.log('Production mode:', environment.production);
}
```

## Next Steps

1. **Update your production URL** in `src/environments/environment.prod.ts`
2. **Test locally** with `ng serve` (should connect to localhost:5000)
3. **Build for production** with `ng build`
4. **Deploy** the `dist/` folder to your hosting provider

---

Your code is now environment-aware and ready for both local development and production deployment! 🚀
