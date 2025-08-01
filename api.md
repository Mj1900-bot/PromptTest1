# Comprehensive API Documentation for a Cat App

---

## Table of Contents
1. [Introduction](#introduction)
2. [Getting Started](#getting-started)
3. [API Endpoints](#api-endpoints)
4. [Authentication](#authentication)
5. [React/TypeScript Integration](#reacttypescript-integration)
6. [Error Handling](#error-handling)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)
9. [Appendix](#appendix)

---

## 1. Introduction

### 1.1 Overview
This documentation provides a detailed guide for building a **Cat App** using **React/TypeScript**. The app will interact with a backend API to fetch cat facts, images, and manage user interactions (e.g., saving favorites). The API is designed for simplicity, scalability, and ease of integration.

### 1.2 Key Features
- Fetch random cat facts.
- Retrieve cat images from a public API.
- User authentication and favorite management.
- Responsive UI for web and mobile.

### 1.3 Target Audience
- Frontend developers using React/TypeScript.
- Backend developers building the API.
- Product managers overseeing the project.

---

## 2. Getting Started

### 2.1 Prerequisites
- **Node.js** (v16+)
- **npm** or **yarn**
- **React** (v18+)
- **TypeScript** (v4.5+)
- **Axios** for API calls
- **JSON Server** (for mock backend)

### 2.2 Project Setup
1. **Initialize the React App**:
   ```bash
   npx create-react-app cat-app --template typescript
   cd cat-app
   ```

2. **Install Dependencies**:
   ```bash
   npm install axios json-server
   ```

3. **Directory Structure**:
   ```
   src/
   ├── components/
   ├── services/
   ├── types/
   ├── App.tsx
   └── index.tsx
   ```

---

## 3. API Endpoints

### 3.1 Base URL
```
https://api.catapp.com/v1
```

### 3.2 Endpoints

#### 3.2.1 Cat Facts
**GET** `/api/cats/facts`

- **Description**: Fetch a random cat fact.
- **Parameters**: None
- **Response**:
  ```json
  {
    "fact": "Cats have 32 muscles that control their ears.",
    "length": 45
  }
  ```

#### 3.2.2 Cat Images
**GET** `/api/cats/images`

- **Description**: Retrieve a random cat image URL.
- **Parameters**: 
  - `size` (optional): `small`, `medium`, `large`
- **Response**:
  ```json
  {
    "url": "https://cdn.catapp.com/images/cat1.jpg",
    "size": "medium"
  }
  ```

#### 3.2.3 User Favorites
**POST** `/api/users/favorites`

- **Description**: Save a favorite cat fact/image pair.
- **Request Body**:
  ```json
  {
    "userId": "123",
    "fact": "Cats can jump up to 5 times their height.",
    "imageUrl": "https://cdn.catapp.com/images/cat2.jpg"
  }
  ```
- **Response**:
  ```json
  {
    "message": "Favorite saved successfully.",
    "id": "fav_456"
  }
  ```

---

## 4. Authentication

### 4.1 Token-Based Authentication
- **Login**:
  **POST** `/api/auth/login`
  - **Request Body**:
    ```json
    {
      "email": "user@example.com",
      "password": "password123"
    }
    ```
  - **Response**:
    ```json
    {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
      "userId": "123"
    }
    ```

- **Token Storage**:
  Use `localStorage` in React:
  ```typescript
  localStorage.setItem('token', response.data.token);
  ```

### 4.2 Axios Interceptors
Add token to all requests:
```typescript
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://api.catapp.com/v1',
});

api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});
```

---

## 5. React/TypeScript Integration

### 5.1 TypeScript Interfaces
Define types for API responses:
```typescript
// src/types/cat.ts
export interface CatFact {
  fact: string;
  length: number;
}

export interface CatImage {
  url: string;
  size: 'small' | 'medium' | 'large';
}
```

### 5.2 Fetching Data in a Component
Example: Fetching a cat fact:
```tsx
// src/components/CatFact.tsx
import React, { useEffect, useState } from 'react';
import { api } from '../services/api';
import { CatFact } from '../types/cat';

const CatFactComponent: React.FC = () => {
  const [fact, setFact] = useState<CatFact | null>(null);

  useEffect(() => {
    api.get<CatFact>('/api/cats/facts')
      .then(response => setFact(response.data))
      .catch(error => console.error('Error fetching cat fact:', error));
  }, []);

  return (
    <div>
      {fact ? <p>{fact.fact}</p> : <p>Loading...</p>}
    </div>
  );
};
```

### 5.3 State Management
Use `useState` and `useContext` for local state:
```typescript
// src/context/AuthContext.tsx
import React, { createContext, useContext, useState } from 'react';

interface AuthContextType {
  isAuthenticated: boolean;
  login: (token: string) => void;
  logout: () => void;
}

const AuthContext = createContext<AuthContextType | undefined>(undefined);

export const AuthProvider: React.FC = ({ children }) => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  const login = (token: string) => {
    localStorage.setItem('token', token);
    setIsAuthenticated(true);
  };

  const logout = () => {
    localStorage.removeItem('token');
    setIsAuthenticated(false);
  };

  return (
    <AuthContext.Provider value={{ isAuthenticated, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within an AuthProvider');
  }
  return context;
};
```

---

## 6. Error Handling

### 6.1 API Error Responses
- **401 Unauthorized**: Missing or invalid token.
- **404 Not Found**: Invalid endpoint.
- **500 Internal Server Error**: Backend failure.

### 6.2 Handling Errors in React
Wrap API calls in try/catch:
```typescript
try {
  const response = await api.get('/api/cats/facts');
  setFact(response.data);
} catch (error) {
  if (axios.isAxiosError(error)) {
    console.error('API Error:', error.response?.data);
  } else {
    console.error('Unexpected Error:', error);
  }
}
```

---

## 7. Best Practices

### 7.1 Code Organization
- Keep components, services, and types in separate directories.
- Use functional components and hooks.

### 7.2 Performance Optimization
- Use `React.memo` for large components.
- Implement lazy loading for images:
  ```tsx
  <img src={catImage.url} loading="lazy" alt="Cat" />
  ```

### 7.3 Security
- Always validate user input.
- Use HTTPS for API calls.
- Avoid storing sensitive data in `localStorage`.

---

## 8. Troubleshooting

### 8.1 Common Issues

#### 8.1.1 CORS Errors
**Solution**: Configure the backend to allow the frontend origin:
```javascript
// backend/middleware/cors.js
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', 'https://catapp.com');
  next();
});
```

#### 8.1.2 Token Expired
**Solution**: Implement token refresh logic:
```typescript
api.interceptors.response.use(
  response => response,
  async (error) => {
    if (error.response?.status === 401) {
      // Refresh token logic
    }
    return Promise.reject(error);
  }
);
```

---

## 9. Appendix

### 9.1 Mock API Setup
Use **JSON Server** for rapid prototyping:
```json
// db.json
{
  "cats": [
    {
      "id": 1,
      "fact": "Cats can rotate their ears 180 degrees.",
      "image": "https://cdn.catapp.com/images/cat1.jpg"
    }
  ]
}
```

Start the server:
```bash
json-server --watch db.json --port 3001
```

### 9.2 Testing with Postman
- **GET** `http://localhost:3001/cats/facts`
- **POST** `http://localhost:3001/users/favorites` with JSON body.

---

## Conclusion
This documentation provides a complete guide for building a cat app with React/TypeScript. By following the outlined structure, developers can efficiently implement features, integrate APIs, and ensure a robust user experience. For further assistance, refer to the [GitHub repository](https://github.com/catapp) or contact the development team.