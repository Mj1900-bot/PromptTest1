# Intermediate Guide: Building a Cat App with React and TypeScript  

## Introduction  

In this guide, we will walk through the process of building a **cat-themed application** using **React** and **TypeScript**. This project is designed for **cat lovers, pet owners, and animal enthusiasts** who want to explore a digital platform dedicated to feline companions. The app will feature **cat profiles, adoption information, and a community forum** where users can share their experiences and connect with fellow cat enthusiasts.  

The primary goal of this project is to provide a **user-friendly, responsive, and interactive web application** that showcases the beauty and charm of cats while offering valuable resources for cat owners. The app will be built using **React**, a popular JavaScript library for building user interfaces, and **TypeScript**, a statically-typed superset of JavaScript that enhances code reliability and maintainability.  

This guide is intended for **intermediate developers** who have a basic understanding of React and JavaScript. It will cover essential topics such as **project setup, UI design, state management, routing, API integration, and deployment**. By the end of this guide, you will have a fully functional cat app that you can further expand and customize.  

The app will be structured into **several core features**, including:  
- **Cat Profiles**: Display information about different cat breeds and individual cats.  
- **Adoption Information**: Provide resources for cat adoption and care.  
- **Community Forum**: Allow users to share stories, photos, and advice about their cats.  

This guide will provide **step-by-step instructions**, **code examples**, and **best practices** to help you build a scalable and maintainable application. Whether you're building this app for fun or as a portfolio project, this guide will equip you with the knowledge and tools to succeed.

## Project Setup and Configuration  

Before diving into the development process, it's essential to set up the project structure and configure the necessary tools. This guide will use **React** with **TypeScript** to build the application, leveraging the **Create React App (CRA)** tool for a streamlined setup.  

### Initializing the Project  

To begin, open your terminal and run the following command to create a new React project with TypeScript support:  

```bash
npx create-react-app cat-app --template typescript
```

This command will generate a new React project with TypeScript preconfigured. Once the installation is complete, navigate into the project directory:  

```bash
cd cat-app
```

### Installing Dependencies  

Next, install any additional dependencies that will be used throughout the project. For this application, we'll use **React Router** for navigation and **Axios** for API requests. Install them using the following command:  

```bash
npm install react-router-dom axios
```

### Project Structure  

A well-organized project structure is crucial for maintainability. Create the following folder structure within the `src` directory:  

```
src/
├── components/          # Reusable UI components
├── pages/               # Page-level components
├── services/            # API and data services
├── types/               # TypeScript interfaces and types
├── App.tsx              # Main application component
├── index.tsx            # Entry point
```

This structure will help keep the codebase clean and modular as the application grows.  

### Configuring TypeScript  

TypeScript provides strong typing and improved code reliability. To ensure a smooth development experience, configure TypeScript by updating the `tsconfig.json` file with the following settings:  

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "ESNext",
    "jsx": "react-jsx",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "moduleResolution": "node",
    "baseUrl": "./src",
    "paths": {
      "@components/*": ["components/*"],
      "@pages/*": ["pages/*"],
      "@services/*": ["services/*"],
      "@types/*": ["types/*"]
    }
  },
  "include": ["src"]
}
```

These settings enable **strict type checking**, **ES6+ features**, and **modular imports** using path aliases. This configuration will make it easier to reference components and services throughout the application.  

With the project structure and TypeScript configuration in place, the next step is to begin designing the user interface and implementing the core features of the cat app.

## Designing the User Interface  

A well-designed user interface (UI) is essential for creating an engaging and intuitive cat app. The UI should be **responsive**, **visually appealing**, and **easy to navigate**. In this section, we will outline the **layout structure**, **component hierarchy**, and **styling approach** to ensure a consistent and user-friendly experience.  

### Layout Structure  

The app will follow a **single-page application (SPA)** structure with a **header**, **sidebar**, and **main content area**. The header will contain the **logo**, **navigation links**, and **user profile**. The sidebar will provide **quick access to key sections** such as cat profiles, adoption information, and the community forum. The main content area will dynamically render the selected page based on the user's navigation.  

Here's an example of the layout structure in `App.tsx`:  

```tsx
import React from 'react';
import Header from '@components/Header';
import Sidebar from '@components/Sidebar';
import MainContent from '@components/MainContent';

const App: React.FC = () => {
  return (
    <div className="app-container">
      <Header />
      <div className="app-body">
        <Sidebar />
        <MainContent />
      </div>
    </div>
  );
};

export default App;
```

This structure ensures a **consistent layout** across all pages and allows for **easy navigation** between different sections of the app.  

### Component Hierarchy  

To maintain a **modular and reusable codebase**, the UI will be built using a **component-based architecture**. Each section of the app will be broken down into **smaller, self-contained components** that can be reused and tested independently.  

For example, the **cat profile section** will consist of the following components:  
- `CatProfileCard`: Displays information about a specific cat.  
- `CatGallery`: Renders a grid of cat profile cards.  
- `CatDetails`: Shows detailed information about a selected cat.  

By organizing the UI into reusable components, the app becomes **easier to maintain** and **extend** in the future.  

### Styling Approach  

To ensure a **consistent and responsive design**, we will use **Tailwind CSS** for styling. Tailwind provides a **utility-first approach**, allowing developers to apply styles directly in the JSX without writing custom CSS.  

Install Tailwind CSS by running the following command:  

```bash
npm install tailwindcss
```

Then, create a `tailwind.config.js` file and update the `index.css` file to include Tailwind's base styles:  

```css
/* index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

With Tailwind configured, we can now apply responsive styles to our components. For example, the `Header` component can be styled as follows:  

```tsx
import React from 'react';

const Header: React.FC = () => {
  return (
    <header className="bg-blue-600 text-white p-4 shadow-md">
      <div className="container mx-auto flex justify-between items-center">
        <h1 className="text-2xl font-bold">Cat App</h1>
        <nav>
          <ul className="flex space-x-4">
            <li><a href="#" className="hover:underline">Home</a></li>
            <li><a href="#" className="hover:underline">Cats</a></li>
            <li><a href="#" className="hover:underline">Forum</a></li>
          </ul>
        </nav>
      </div>
    </header>
  );
};

export default Header;
```

This approach ensures that the UI is **visually appealing**, **responsive**, and **easy to maintain** as the app grows.

## Implementing Core Features  

With the project structure and UI design in place, it's time to implement the core features of the cat app. The app will include **cat profiles**, **adoption information**, and a **community forum**. Each of these features will be built using **React components** and **TypeScript interfaces** to ensure a clean and maintainable codebase.  

### Cat Profiles  

The **cat profile feature** will allow users to view information about different cat breeds and individual cats. Each profile will include a **photo**, **name**, **age**, **breed**, and **description**.  

To implement this feature, create a `CatProfile` component that accepts a `Cat` interface as a prop. The `Cat` interface will define the structure of the data:  

```ts
// types/Cat.ts
export interface Cat {
  id: number;
  name: string;
  age: number;
  breed: string;
  imageUrl: string;
  description: string;
}
```

Next, create the `CatProfile` component:  

```tsx
// components/CatProfile.tsx
import React from 'react';
import { Cat } from '@types/Cat';

interface CatProfileProps {
  cat: Cat;
}

const CatProfile: React.FC<CatProfileProps> = ({ cat }) => {
  return (
    <div className="cat-profile p-4 border rounded shadow-md">
      <img src={cat.imageUrl} alt={cat.name} className="w-full h-48 object-cover rounded-t" />
      <h2 className="text-xl font-bold mt-2">{cat.name}</h2>
      <p className="text-gray-600">Breed: {cat.breed}</p>
      <p className="text-gray-600">Age: {cat.age} years</p>
      <p className="mt-2">{cat.description}</p>
    </div>
  );
};

export default CatProfile;
```

This component will render a **card-style profile** for each cat, displaying the **image**, **name**, **breed**, **age**, and **description**.  

To display multiple cat profiles, create a `CatGallery` component that maps over an array of `Cat` objects and renders a `CatProfile` for each one:  

```tsx
// components/CatGallery.tsx
import React from 'react';
import CatProfile from './CatProfile';
import { Cat } from '@types/Cat';

interface CatGalleryProps {
  cats: Cat[];
}

const CatGallery: React.FC<CatGalleryProps> = ({ cats }) => {
  return (
    <div className="cat-gallery grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {cats.map((cat) => (
        <CatProfile key={cat.id} cat={cat} />
      ))}
    </div>
  );
};

export default CatGallery;
```

This component uses a **responsive grid layout** to display the cat profiles, ensuring that the app looks great on different screen sizes.  

### Adoption Information  

The **adoption information feature** will provide users with **guidance on adopting a cat**, including **tips for choosing the right cat**, **preparation for adoption**, and **legal considerations**.  

Create a `AdoptionInfo` component that displays this information in a structured format:  

```tsx
// components/AdoptionInfo.tsx
import React from 'react';

const AdoptionInfo: React.FC = () => {
  return (
    <div className="adoption-info p-6 bg-gray-100 rounded shadow-md">
      <h2 className="text-2xl font-bold mb-4">Adopting a Cat</h2>
      <p className="mb-4">
        Adopting a cat is a rewarding experience, but it's important to choose the right cat for your lifestyle.
      </p>
      <h3 className="text-xl font-semibold mb-2">Tips for Choosing a Cat</h3>
      <ul className="list-disc pl-5 mb-4">
        <li>Consider your living space and activity level.</li>
        <li>Research different cat breeds and their characteristics.</li>
        <li>Visit local shelters and rescue organizations.</li>
      </ul>
      <h3 className="text-xl font-semibold mb-2">Preparation for Adoption</h3>
      <ul className="list-disc pl-5 mb-4">
        <li>Ensure your home is cat-friendly with safe spaces and toys.</li>
        <li>Set up a feeding and litter schedule.</li>
        <li>Prepare for regular veterinary checkups.</li>
      </ul>
    </div>
  );
};

export default AdoptionInfo;
```

This component provides a **clear and informative guide** for users who are considering adopting a cat.  

### Community Forum  

The **community forum feature** will allow users to **share stories**, **ask questions**, and **connect with other cat lovers**. The forum will include a **list of posts**, a **post creation form**, and a **comment section**.  

Start by creating a `ForumPost` component that represents a single forum post:  

```tsx
// components/ForumPost.tsx
import React from 'react';

interface ForumPost {
  id: number;
  author: string;
  content: string;
  date: string;
}

interface ForumPostProps {
  post: ForumPost;
}

const ForumPost: React.FC<ForumPostProps> = ({ post }) => {
  return (
    <div className="forum-post p-4 border rounded shadow-md mb-4">
      <div className="flex justify-between">
        <h3 className="font-bold">{post.author}</h3>
        <span className="text-sm text-gray-500">{post.date}</span>
      </div>
      <p className="mt-2">{post.content}</p>
    </div>
  );
};

export default ForumPost;
```

Next, create a `ForumList` component that displays a list of forum posts:  

```tsx
// components/ForumList.tsx
import React from 'react';
import ForumPost from './ForumPost';

interface ForumListProps {
  posts: ForumPost[];
}

const ForumList: React.FC<ForumListProps> = ({ posts }) => {
  return (
    <div className="forum-list">
      {posts.map((post) => (
        <ForumPost key={post.id} post={post} />
      ))}
    </div>
  );
};

export default ForumList;
```

Finally, create a `ForumForm` component that allows users to submit new posts:  

```tsx
// components/ForumForm.tsx
import React, { useState } from 'react';

interface ForumFormProps {
  onPostSubmit: (post: ForumPost) => void;
}

const ForumForm: React.FC<ForumFormProps> = ({ onPostSubmit }) => {
  const [author, setAuthor] = useState('');
  const [content, setContent] = useState('');

  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    const newPost: ForumPost = {
      id: Date.now(),
      author,
      content,
      date: new Date().toLocaleDateString(),
    };
    onPostSubmit(newPost);
    setAuthor('');
    setContent('');
  };

  return (
    <form onSubmit={handleSubmit} className="forum-form p-4 bg-white rounded shadow-md mb-4">
      <h3 className="text-xl font-bold mb-2">Create a Post</h3>
      <div className="mb-2">
        <label className="block mb-1">Author</label>
        <input
          type="text"
          value={author}
          onChange={(e) => setAuthor(e.target.value)}
          className="w-full p-2 border rounded"
          required
        />
      </div>
      <div className="mb-2">
        <label className="block mb-1">Content</label>
        <textarea
          value={content}
          onChange={(e) => setContent(e.target.value)}
          className="w-full p-2 border rounded"
          rows={4}
          required
        />
      </div>
      <button type="submit" className="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
        Submit
      </button>
    </form>
  );
};

export default ForumForm;
```

This form allows users to **submit new forum posts**, which can then be added to the `ForumList` component.  

By implementing these core features, the cat app becomes a **functional and interactive platform** for cat lovers to explore, learn, and connect.

## Managing Application State  

Effective state management is crucial for building a scalable and maintainable React application. In this section, we will explore how to manage the application state using **React Context API** and **useReducer** to handle complex state logic. These tools will help us manage the **cat data**, **user authentication**, and **forum posts** in a centralized and organized manner.  

### React Context API for Global State  

The **React Context API** provides a way to share state across multiple components without manually passing props down the component tree. This is particularly useful for managing **global state** such as **user authentication**, **cat profiles**, and **forum data**.  

To create a context for the cat app, start by defining a **context file** that includes the state and functions for updating it:  

```ts
// context/CatContext.ts
import React, { createContext, useContext, useReducer } from 'react';
import { Cat } from '@types/Cat';
import { ForumPost } from '@types/Forum';

interface State {
  cats: Cat[];
  forumPosts: ForumPost[];
  isAuthenticated: boolean;
}

type Action =
  | { type: 'SET_CATS'; payload: Cat[] }
  | { type: 'ADD_FORUM_POST'; payload: ForumPost }
  | { type: 'SET_AUTH'; payload: boolean };

const initialState: State = {
  cats: [],
  forumPosts: [],
  isAuthenticated: false,
};

const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case 'SET_CATS':
      return { ...state, cats: action.payload };
    case 'ADD_FORUM_POST':
      return { ...state, forumPosts: [...state.forumPosts, action.payload] };
    case 'SET_AUTH':
      return { ...state, isAuthenticated: action.payload };
    default:
      return state;
  }
};

const CatContext = createContext<{
  state: State;
  dispatch: React.Dispatch<Action>;
}>({ state: initialState, dispatch: () => null });

export const useCatContext = () => useContext(CatContext);

export const CatProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);
  return <CatContext.Provider value={{ state, dispatch }}>{children}</CatContext.Provider>;
};
```

This context defines a **state object** that includes **cats**, **forum posts**, and **authentication status**, along with a **reducer function** to handle state updates. The `CatProvider` component wraps the application and makes the state and dispatch function available to all child components.  

To use the context in a component, import the `useCatContext` hook and access the state and dispatch function:  

```tsx
// components/CatGallery.tsx
import React from 'react';
import { useCatContext } from '@context/CatContext';
import CatProfile from './CatProfile';

const CatGallery: React.FC = () => {
  const { state } = useCatContext();

  return (
    <div className="cat-gallery grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {state.cats.map((cat) => (
        <CatProfile key={cat.id} cat={cat} />
      ))}
    </div>
  );
};

export default CatGallery;
```

This example demonstrates how to access the **global cat state** and render the **CatGallery** component based on the current state.  

### Managing Authentication State  

User authentication is a common requirement for applications that include **user accounts**, **login functionality**, or **personalized content**. In this app, we will use the **CatContext** to manage the **authentication state** and provide **login/logout functionality**.  

Create an `AuthProvider` component that wraps the application and manages the authentication state:  

```tsx
// context/AuthContext.ts
import React, { createContext, useContext, useState } from 'react';

interface AuthContextType {
  isAuthenticated: boolean;
  login: () => void;
  logout: () => void;
}

const AuthContext = createContext<AuthContextType>({
  isAuthenticated: false,
  login: () => {},
  logout: () => {},
});

export const useAuth = () => useContext(AuthContext);

export const AuthProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  const login = () => {
    setIsAuthenticated(true);
  };

  const logout = () => {
    setIsAuthenticated(false);
  };

  return (
    <AuthContext.Provider value={{ isAuthenticated, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};
```

This component provides **login and logout functions** that can be used in the app's UI to control access to certain features.  

To use the authentication context in a component, import the `useAuth` hook and call the `login` or `logout` functions as needed:  

```tsx
// components/AuthButton.tsx
import React from 'react';
import { useAuth } from '@context/AuthContext';

const AuthButton: React.FC = () => {
  const { isAuthenticated, login, logout } = useAuth();

  return (
    <div>
      {isAuthenticated ? (
        <button onClick={logout}>Logout</button>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </div>
  );
};

export default AuthButton;
```

This example demonstrates how to **conditionally render login/logout buttons** based on the user's authentication status.  

By leveraging the **React Context API** and **useReducer**, the cat app can efficiently manage **global state**, **authentication**, and **user interactions** in a clean and maintainable way.

## Implementing Routing and Navigation  

To enable seamless navigation between different sections of the cat app, we will use **React Router** to manage routing. React Router allows us to define **routes** for different pages and components, making it easy to navigate between the **home page**, **cat profiles**, **adoption information**, and **community forum**.  

### Setting Up React Router  

First, install **React Router** if it hasn't already been added to the project:  

```bash
npm install react-router-dom
```

Next, update the `App.tsx` file to include the **BrowserRouter** and define the **routes** for the application:  

```tsx
// App.tsx
import React from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Home from '@pages/Home';
import CatProfile from '@pages/CatProfile';
import AdoptionInfo from '@pages/AdoptionInfo';
import Forum from '@pages/Forum';

const App: React.FC = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/cats/:id" element={<CatProfile />} />
        <Route path="/adoption" element={<AdoptionInfo />} />
        <Route path="/forum" element={<Forum />} />
      </Routes>
    </Router>
  );
};

export default App;
```

This configuration defines **four routes**:  
- **Home (`/`)**: Displays the main page with a list of cat profiles.  
- **Cat Profile (`/cats/:id`)**: Displays detailed information about a specific cat.  
- **Adoption Info (`/adoption`)**: Provides information about cat adoption.  
- **Forum (`/forum`)**: Displays the community forum.  

### Creating Navigation Links  

To allow users to navigate between these routes, create a **navigation bar** that includes links to each section of the app. Update the `Header` component to include **navigation links** using the `Link` component from React Router:  

```tsx
// components/Header.tsx
import React from 'react';
import { Link } from 'react-router-dom';

const Header: React.FC = () => {
  return (
    <header className="bg-blue-600 text-white p-4 shadow-md">
      <div className="container mx-auto flex justify-between items-center">
        <h1 className="text-2xl font-bold">Cat App</h1>
        <nav>
          <ul className="flex space-x-4">
            <li><Link to="/" className="hover:underline">Home</Link></li>
            <li><Link to="/adoption" className="hover:underline">Adoption</Link></li>
            <li><Link to="/forum" className="hover:underline">Forum</Link></li>
          </ul>
        </nav>
      </div>
    </header>
  );
};

export default Header;
```

This navigation bar provides **direct links** to the main sections of the app, making it easy for users to **browse cat profiles**, **access adoption information**, and **participate in the forum**.  

### Nested Routes for Cat Profiles  

To display individual cat profiles, we need to define a **nested route** that includes the **cat ID** as a parameter. Update the `CatProfile` page to fetch and display the selected cat's information based on the route parameter:  

```tsx
// pages/CatProfile.tsx
import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';
import { useCatContext } from '@context/CatContext';
import { Cat } from '@types/Cat';

const CatProfile: React.FC = () => {
  const { id } = useParams<{ id: string }>();
  const { state } = useCatContext();
  const [cat, setCat] = useState<Cat | null>(null);

  useEffect(() => {
    const selectedCat = state.cats.find((c) => c.id === parseInt(id, 10));
    if (selectedCat) {
      setCat(selectedCat);
    }
  }, [id, state.cats]);

  if (!cat) {
    return <div>Cat not found</div>;
  }

  return (
    <div className="cat-profile p-6 bg-white rounded shadow-md">
      <img src={cat.imageUrl} alt={cat.name} className="w-full h-64 object-cover rounded-t" />
      <h2 className="text-2xl font-bold mt-2">{cat.name}</h2>
      <p className="text-gray-600">Breed: {cat.breed}</p>
      <p className="text-gray-600">Age: {cat.age} years</p>
      <p className="mt-4">{cat.description}</p>
    </div>
  );
};

export default CatProfile;
```

This component uses the **`useParams`** hook to extract the **cat ID** from the route and fetch the corresponding cat from the global state. If the cat is found, it is displayed with its **image**, **name**, **breed**, **age**, and **description**.  

By implementing **React Router**, the cat app now supports **smooth navigation** between different sections, enhancing the **user experience** and making the app more **interactive and user-friendly**.

## Integrating External APIs  

To enhance the functionality of the cat app, we can integrate **external APIs** to fetch **cat data**, **adoption information**, and **community forum posts**. APIs provide a convenient way to access **real-time data** and **third-party services**, making the app more **interactive and dynamic**. In this section, we will explore how to **fetch cat data** from an external API and **display it in the app** using **Axios** and **React components**.  

### Fetching Cat Data from an API  

One of the most popular APIs for cat-related data is the **The Cat API** (https://thecatapi.com/). This API provides a **collection of cat images**, **breed information**, and **random cat facts**. To use this API, we first need to **register for an API key** and then **make requests** to fetch the data.  

Install **Axios**, a popular HTTP client for making API requests:  

```bash
npm install axios
```

Next, create a **service file** to handle API requests. Create a new file called `CatService.ts` in the `services` directory:  

```ts
// services/CatService.ts
import axios from 'axios';

const API_KEY = 'YOUR_API_KEY'; // Replace with your actual API key
const BASE_URL = 'https://api.thecatapi.com/v1';

const catService = axios.create({
  baseURL: BASE_URL,
  headers: {
    'Content-Type': 'application/json',
    'x-api-key': API_KEY,
  },
});

export const fetchCats = async () => {
  try {
    const response = await catService.get('/images/search?limit=10');
    return response.data;
  } catch (error) {
    console.error('Error fetching cats:', error);
    return [];
  }
};

export const fetchCatById = async (id: string) => {
  try {
    const response = await catService.get(`/images/${id}`);
    return response.data;
  } catch (error) {
    console.error('Error fetching cat by ID:', error);
    return null;
  }
};
```

This service file defines two functions:  
- `fetchCats()`: Fetches a list of 10 random cat images.  
- `fetchCatById(id)`: Fetches a specific cat image by ID.  

### Displaying API Data in the App  

To display the fetched cat data in the app, update the `CatGallery` component to use the `fetchCats()` function from the `CatService`. Modify the `CatGallery` component as follows:  

```tsx
// components/CatGallery.tsx
import React, { useEffect, useState } from 'react';
import { fetchCats } from '@services/CatService';
import CatProfile from './CatProfile';

const CatGallery: React.FC = () => {
  const [cats, setCats] = useState<any[]>([]);

  useEffect(() => {
    fetchCats().then((data) => {
      setCats(data);
    });
  }, []);

  return (
    <div className="cat-gallery grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      {cats.map((cat) => (
        <CatProfile key={cat.id} cat={cat} />
      ))}
    </div>
  );
};

export default CatGallery;
```

This component uses the `fetchCats()` function to retrieve cat data from the API and displays it using the `CatProfile` component.  

### Displaying Individual Cat Profiles  

To display a specific cat profile based on the route parameter, update the `CatProfile` page to use the `fetchCatById()` function:  

```tsx
// pages/CatProfile.tsx
import React, { useEffect, useState } from 'react';
import { useParams } from 'react-router-dom';
import { fetchCatById } from '@services/CatService';

const CatProfile: React.FC = () => {
  const { id } = useParams<{ id: string }>();
  const [cat, setCat] = useState<any | null>(null);

  useEffect(() => {
    if (id) {
      fetchCatById(id).then((data) => {
        setCat(data);
      });
    }
  }, [id]);

  if (!cat) {
    return <div>Cat not found</div>;
  }

  return (
    <div className="cat-profile p-6 bg-white rounded shadow-md">
      <img src={cat.url} alt="Cat" className="w-full h-64 object-cover rounded-t" />
      <h2 className="text-2xl font-bold mt-2">Cat ID: {cat.id}</h2>
      <p className="text-gray-600">Breed: {cat.breed?.name || 'Unknown'}</p>
      <p className="mt-4">{cat.description || 'No description available.'}</p>
    </div>
  );
};

export default CatProfile;
```

This component fetches a specific cat by ID and displays its **image**, **ID**, **breed**, and **description**.  

By integrating external APIs, the cat app can now **fetch real-time data** and provide users with **up-to-date information** about different cat breeds and images. This enhances the **user experience** and makes the app more **interactive and engaging**.

## Testing and Debugging the Application  

Testing and debugging are essential steps in the development process to ensure the application functions correctly and is free of errors. In this section, we will explore how to **write unit tests** for the app's components and **debug common issues** that may arise during development.  

### Writing Unit Tests  

Unit testing helps verify that