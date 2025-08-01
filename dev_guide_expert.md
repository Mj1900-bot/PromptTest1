# Expert Guide to Building a Cat App with React and TypeScript

## Introduction to the Cat App Project

The Cat App project is a small-scale application designed to provide users with a fun and engaging way to interact with cat-related content. This application leverages the power of React, a popular JavaScript library for building user interfaces, and TypeScript, a statically-typed superset of JavaScript, to create a robust and maintainable codebase. The primary objective of the Cat App is to showcase cat images, names, and other relevant information, while also allowing users to interact with the content through features such as liking, sharing, or saving their favorite cats. By combining React's component-based architecture with TypeScript's type-checking capabilities, the Cat App ensures a seamless development experience and a high-quality user interface.

The Cat App is particularly well-suited for developers who are looking to build a simple yet effective web application. Its small scale and straightforward complexity make it an ideal project for those who are new to React and TypeScript or for those who want to reinforce their understanding of these technologies. The application can be hosted on various platforms, making it accessible to users across different devices and browsers. Additionally, the Cat App serves as a great foundation for learning key concepts in modern web development, such as state management, component composition, and API integration.

The use of React in this project allows for the creation of reusable UI components, which simplifies the development process and enhances the maintainability of the code. React's virtual DOM ensures efficient updates and rendering, resulting in a responsive and smooth user experience. On the other hand, TypeScript adds an extra layer of type safety, reducing the likelihood of runtime errors and making the codebase more predictable and easier to debug. Together, these technologies enable developers to build a scalable and reliable application, even for a small project like the Cat App.

The Cat App project also emphasizes the importance of good design practices and user experience. The application's interface is intended to be intuitive and visually appealing, encouraging users to explore and interact with the content. By focusing on simplicity and clarity, the Cat App ensures that users can easily navigate through the features and enjoy the experience of discovering new cat images and information. This guide will walk through the entire development process, from setting up the project to deploying the final application, providing practical insights and code examples to help developers create a successful Cat App.

## Project Setup and Configuration

To begin building the Cat App, the first step is to set up the project environment using React and TypeScript. This process involves initializing a new React project, installing necessary dependencies, and configuring TypeScript to ensure a smooth development experience. The following steps outline the setup process in detail.

### Initializing the React Project

The foundation of the Cat App is a React project. To create a new React application, you can use the Create React App (CRA) tool, which provides a zero-configuration setup for React projects. CRA simplifies the process by handling all the necessary build configurations, allowing developers to focus on writing code. To initialize the project, open your terminal and run the following command:

```bash
npx create-react-app cat-app --template typescript
```

This command creates a new React project named "cat-app" with TypeScript as the default template. CRA automatically installs React, React DOM, and other essential dependencies, including TypeScript and its type definitions for React. Once the project is created, navigate to the project directory:

```bash
cd cat-app
```

### Installing Dependencies

After initializing the project, the next step is to install any additional dependencies required for the Cat App. While CRA includes many default dependencies, you may need to add specific libraries for features such as routing, state management, or API calls. For example, if you plan to implement routing for different cat profiles, you can install React Router:

```bash
npm install react-router-dom
```

If you need to manage state more effectively, consider installing Redux Toolkit:

```bash
npm install @reduxjs/toolkit react-redux
```

For API calls, Axios is a popular choice for making HTTP requests:

```bash
npm install axios
```

These dependencies will enhance the functionality of the Cat App and provide a more robust development environment.

### Configuring TypeScript

TypeScript is already configured in the CRA setup, but it's essential to understand the configuration files to ensure they meet the project's needs. The primary configuration file for TypeScript is `tsconfig.json`, which is automatically generated when you create a React project with TypeScript. This file contains various settings that affect how TypeScript compiles the code. Some key configurations include:

- **`target`**: Specifies the ECMAScript version to compile to. The default is usually `es5`, but you can set it to a higher version if needed.
- **`module`**: Defines the module code generation. The default is `esnext`, which is suitable for modern browsers.
- **`jsx`**: Determines how JSX is handled. The default is `react-jsx`, which is appropriate for React projects.
- **`strict`**: Enables strict type-checking options. It's recommended to keep this enabled to catch potential errors early.

You can customize these settings based on your project requirements. For instance, if you want to use the latest JavaScript features, you can update the `target` and `module` settings accordingly. Additionally, you may want to configure the `include` and `exclude` fields to specify which files should be included in the TypeScript compilation process.

### Folder Structure

Organizing the project structure is crucial for maintainability and scalability. A typical folder structure for the Cat App might look like this:

```
src/
├── components/
│   ├── CatCard.tsx
│   └── Header.tsx
├── pages/
│   ├── HomePage.tsx
│   └── CatDetailPage.tsx
├── services/
│   └── catService.ts
├── types/
│   └── catTypes.ts
├── App.tsx
└── index.tsx
```

This structure separates components, pages, services, and types into distinct folders, making it easier to manage the codebase as the project grows. Each component and page can be developed independently, promoting reusability and modularity.

### Conclusion

By following these steps, you can set up a solid foundation for the Cat App project. The combination of React and TypeScript provides a powerful environment for building a user-friendly application that showcases cat-related content. With the project initialized, dependencies installed, and TypeScript configured, you are now ready to start developing the core features of the Cat App. This setup ensures that you can focus on creating engaging user experiences while benefiting from the type safety and performance optimizations that TypeScript offers. As you progress through the development process, remember to maintain a clean and organized code structure to facilitate future enhancements and troubleshooting. 😊

## Designing the User Interface for the Cat App

Designing an intuitive and visually appealing user interface (UI) is crucial for the success of the Cat App. A well-structured UI not only enhances user experience but also makes the application more engaging and easier to navigate. In this section, we will explore the key components of the UI, including the layout, color scheme, typography, and the implementation of a cat card component using React and TypeScript. We will also provide practical code examples to illustrate how these elements can be brought to life.

### Layout and Structure

The layout of the Cat App should be clean and organized, allowing users to easily find and interact with the content. A common approach is to use a grid or flexbox layout to display cat cards. This layout enables a responsive design that adapts to different screen sizes, ensuring that the app is accessible on both desktop and mobile devices.

For the main layout, consider using a container that holds the header, a section for displaying cat cards, and a footer. The header can include the app's title and navigation links, while the footer can provide additional information or links to social media. Here's a basic example of how you might structure the layout using React components:

```tsx
import React from 'react';
import Header from './components/Header';
import CatCard from './components/CatCard';
import Footer from './components/Footer';

const App: React.FC = () => {
  return (
    <div className="app-container">
      <Header />
      <main className="cat-cards-section">
        <CatCard />
      </main>
      <Footer />
    </div>
  );
};

export default App;
```

In this example, the `App` component serves as the main container, and it includes the `Header`, `CatCard`, and `Footer` components. This modular approach allows for easy updates and maintenance of the UI.

### Color Scheme and Typography

Choosing the right color scheme and typography is essential for creating a cohesive and aesthetically pleasing design. For the Cat App, a soft and warm color palette would be appropriate, as it evokes a sense of comfort and playfulness. Consider using shades of orange, yellow, and white to create a friendly atmosphere.

Typography should be clear and readable. A sans-serif font like Arial or Helvetica can be used for the body text, while a more playful font might be suitable for headings to reflect the app's theme. Here's an example of how you can define the color scheme and typography in your CSS:

```css
/* App.css */
.app-container {
  font-family: 'Arial', sans-serif;
  background-color: #fff8f0;
  color: #8b5e3c;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.header {
  background-color: #f9d949;
  color: #8b5e3c;
  padding: 20px;
  text-align: center;
  font-size: 2em;
  font-weight: bold;
}

.cat-cards-section {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 20px;
  gap: 20px;
}

.cat-card {
  background-color: #fff;
  border: 2px solid #f9d949;
  border-radius: 10px;
  width: 200px;
  padding: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.cat-card:hover {
  transform: scale(1.05);
}
```

This CSS code defines a warm color scheme with a soft orange background for the app container and a contrasting color for the header. The `cat-card` class styles the individual cat cards, making them visually distinct and interactive when hovered over.

### Implementing the Cat Card Component

The cat card component is the heart of the Cat App, as it displays the cat's image, name, and other relevant information. This component should be reusable, allowing for easy addition of new cat cards in the future. Here's how you can create a `CatCard` component using React and TypeScript:

```tsx
// CatCard.tsx
import React from 'react';

interface CatProps {
  name: string;
  imageUrl: string;
  description: string;
}

const CatCard: React.FC<CatProps> = ({ name, imageUrl, description }) => {
  return (
    <div className="cat-card">
      <img src={imageUrl} alt={name} className="cat-image" />
      <h2 className="cat-name">{name}</h2>
      <p className="cat-description">{description}</p>
    </div>
  );
};

export default CatCard;
```

In this example, the `CatCard` component is defined with a TypeScript interface `CatProps` that specifies the types of the props it receives. The component renders an image, a heading for the cat's name, and a paragraph for the description. This structure allows for easy customization and extension of the component's functionality.

### Responsive Design

Ensuring that the Cat App is responsive is essential for providing a consistent user experience across various devices. You can achieve this by using media queries in your CSS to adjust the layout and styling based on the screen size. For instance, you might want to change the number of cat cards displayed per row on smaller screens:

```css
/* Responsive styles */
@media (max-width: 768px) {
  .cat-cards-section {
    flex-direction: column;
    align-items: center;
  }

  .cat-card {
    width: 90%;
    max-width: 300px;
  }
}
```

These media queries adjust the layout to a single column on screens smaller than 768 pixels, making it more user-friendly on mobile devices. Additionally, the `width` of the cat cards is set to 90% of the container, ensuring they fit well on smaller screens.

### Accessibility Considerations

Accessibility is a vital aspect of UI design. To make the Cat App accessible, ensure that all images have appropriate `alt` attributes, and use semantic HTML elements. For example, the `img` tag in the `CatCard` component should include an `alt` attribute that describes the cat's image:

```tsx
<img src={imageUrl} alt={name} className="cat-image" />
```

This practice helps users with visual impairments understand the content of the images through screen readers.

### Conclusion

Designing the user interface for the Cat App involves careful consideration of layout, color scheme, typography, and the implementation of key components like the cat card. By following these guidelines and using the provided code examples, you can create a visually appealing and user-friendly application that showcases cat-related content effectively. The modular approach to component design, combined with responsive and accessible practices, ensures that the Cat App will provide a delightful experience for all users. 😊

## Core Functionality of the Cat App

The core functionality of the Cat App revolves around fetching and displaying cat data from an external API. This process involves making HTTP requests to retrieve cat information, parsing the response, and rendering the data in a user-friendly manner. In this section, we will walk through the implementation of these features using React and TypeScript, providing practical code examples and explanations to guide you through the development process.

### Fetching Cat Data from an API

To fetch cat data, we can utilize a public API such as The Cat API, which provides a wealth of information about various cat breeds and images. First, we need to make an HTTP GET request to the API endpoint. In React, we can use the `fetch` function or a library like Axios to handle these requests. Here's an example using `fetch` to retrieve cat data:

```tsx
// services/catService.ts
import { useState, useEffect } from 'react';

interface Cat {
  id: string;
  name: string;
  description: string;
  imageUrl: string;
}

const useFetchCats = () => {
  const [cats, setCats] = useState<Cat[]>([]);
  const [loading, setLoading] = useState<boolean>(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    const fetchCats = async () => {
      try {
        const response = await fetch('https://api.thecatapi.com/v1/breeds');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await response.json();
        // Transform the data to fit our Cat interface
        const transformedCats: Cat[] = data.map((cat: any) => ({
          id: cat.id,
          name: cat.name,
          description: cat.description,
          imageUrl: `https://cdn2.thecatapi.com/images/${cat.id}.jpg`,
        }));
        setCats(transformedCats);
        setLoading(false);
      } catch (err) {
        setError(err.message);
        setLoading(false);
      }
    };

    fetchCats();
  }, []);

  return { cats, loading, error };
};

export default useFetchCats;
```

In this code snippet, we define a custom React hook `useFetchCats` that fetches cat data from the API. The hook uses the `useState` and `useEffect` hooks to manage the state of the cats, loading status, and any potential errors. When the component using this hook mounts, it triggers the `fetchCats` function, which makes the GET request to the specified endpoint.

### Displaying Cat Data

Once the data is fetched, the next step is to display it in the UI. We can create a component that utilizes the `useFetchCats` hook to render the list of cats. Here's an example of how to implement this:

```tsx
// components/CatList.tsx
import React from 'react';
import useFetchCats from '../services/catService';
import CatCard from './CatCard';

const CatList: React.FC = () => {
  const { cats, loading, error } = useFetchCats();

  if (loading) {
    return <div>Loading...</div>;
  }

  if (error) {
    return <div>Error: {error}</div>;
  }

  return (
    <div className="cat-list">
      {cats.map((cat) => (
        <CatCard key={cat.id} name={cat.name} imageUrl={cat.imageUrl} description={cat.description} />
      ))}
    </div>
  );
};

export default CatList;
```

In this `CatList` component, we use the `useFetchCats` hook to access the fetched cat data. The component checks the loading and error states and displays appropriate messages. When the data is available, it maps over the `cats` array and renders a `CatCard` component for each cat, passing along the necessary props.

### Implementing the Cat Card Component

The `CatCard` component is responsible for displaying individual cat information. It should accept the cat's name, image URL, and description as props and render them in a visually appealing format. Here's an example implementation:

```tsx
// components/CatCard.tsx
import React from 'react';

interface CatProps {
  name: string;
  imageUrl: string;
  description: string;
}

const CatCard: React.FC<CatProps> = ({ name, imageUrl, description }) => {
  return (
    <div className="cat-card">
      <img src={imageUrl} alt={name} className="cat-image" />
      <h2 className="cat-name">{name}</h2>
      <p className="cat-description">{description}</p>
    </div>
  );
};

export default CatCard;
```

This component uses the `CatProps` interface to define the types of the props it receives. The `img` tag displays the cat's image, while the `h2` and `p` tags show the name and description, respectively. The styling for the `cat-card` class can be defined in a CSS file to enhance the visual presentation.

### Handling User Interactions

To enhance user engagement, we can add interactive features to the Cat App, such as allowing users to like or save their favorite cats. This can be achieved by managing state within the `CatCard` component. Here's an example of how to implement a like feature:

```tsx
// components/CatCard.tsx
import React, { useState } from 'react';

interface CatProps {
  name: string;
  imageUrl: string;
  description: string;
}

const CatCard: React.FC<CatProps> = ({ name, imageUrl, description }) => {
  const [liked, setLiked] = useState<boolean>(false);

  const handleLike = () => {
    setLiked(!liked);
  };

  return (
    <div className="cat-card">
      <img src={imageUrl} alt={name} className="cat-image" />
      <h2 className="cat-name">{name}</h2>
      <p className="cat-description">{description}</p>
      <button onClick={handleLike} className={`like-button ${liked ? 'liked' : ''}`}>
        {liked ? '❤️' : '🤍'}
      </button>
    </div>
  );
};

export default CatCard;
```

In this updated `CatCard` component, we introduce a `liked` state variable and a `handleLike` function that toggles the like status when the button is clicked. The button's appearance changes based on the `liked` state, providing visual feedback to the user.

### Styling the Components

To ensure the Cat App looks appealing, we can add some basic styling to the components. Here's an example of how to style the `CatCard` component:

```css
/* components/CatCard.css */
.cat-card {
  background-color: #fff;
  border: 2px solid #f9d949;
  border-radius: 10px;
  width: 200px;
  padding: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
  text-align: center;
}

.cat-card:hover {
  transform: scale(1.05);
}

.cat-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
  margin-bottom: 10px;
}

.cat-name {
  font-size: 1.5em;
  margin-bottom: 5px;
}

.cat-description {
  font-size: 1em;
  color: #555;
  margin-bottom: 10px;
}

.like-button {
  background-color: #f9d949;
  border: none;
  color: #8b5e3c;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 5px;
}

.like-button.liked {
  background-color: #ff4d4d;
  color: white;
}
```

This CSS code styles the `CatCard` component, making it visually appealing and interactive. The `cat-card` class provides a clean look with a soft orange border and a subtle shadow. The `like-button` class styles the like button, changing its appearance when the user clicks it.

### Conclusion

By implementing the core functionality of the Cat App, you can create an engaging and interactive experience for users. The process of fetching and displaying cat data from an API is straightforward with React and TypeScript, allowing for a robust and maintainable codebase. The `CatCard` component, along with its styling and interactive features, showcases the cat information effectively. As you continue to develop the Cat App, consider adding more features and interactions to enhance the user experience further. 😊

## State Management in the Cat App

State management is a critical aspect of building the Cat App, as it allows for the efficient handling of data and user interactions. In this section, we will explore how to implement state management using the React Context API, which provides a way to share state across all components in a React application without having to pass props down manually at every level. We will also provide code examples to demonstrate the setup and usage of the Context API, ensuring that you can effectively manage the state of your Cat App.

### Creating the Context

To begin, we need to create a context that will hold the state for our Cat App. This context will be used to store and manage the list of cats, the current selected cat, and any other relevant state information. Here's how you can create a new context:

```tsx
// context/CatContext.tsx
import React, { createContext, useContext, useState, useEffect } from 'react';
import { Cat } from '../types/catTypes';

interface CatContextProps {
  cats: Cat[];
  currentCat: Cat | null;
  setCurrentCat: (cat: Cat | null) => void;
}

const CatContext = createContext<CatContextProps | undefined>(undefined);

export const useCatContext = () => {
  const context = useContext(CatContext);
  if (context === undefined) {
    throw new Error('useCatContext must be used within a CatProvider');
  }
  return context;
};

export const CatProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [cats, setCats] = useState<Cat[]>([]);
  const [currentCat, setCurrentCat] = useState<Cat | null>(null);

  useEffect(() => {
    // Fetch cats from an API
    const fetchCats = async () => {
      try {
        const response = await fetch('https://api.thecatapi.com/v1/breeds');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await response.json();
        // Transform the data to fit our Cat interface
        const transformedCats: Cat[] = data.map((cat: any) => ({
          id: cat.id,
          name: cat.name,
          description: cat.description,
          imageUrl: `https://cdn2.thecatapi.com/images/${cat.id}.jpg`,
        }));
        setCats(transformedCats);
      } catch (err) {
        console.error(err);
      }
    };

    fetchCats();
  }, []);

  return (
    <CatContext.Provider value={{ cats, currentCat, setCurrentCat }}>
      {children}
    </CatContext.Provider>
  );
};
```

In this code, we define a `CatContext` using `createContext`, which will be used to provide the state to our components. The `useCatContext` hook is a custom hook that allows components to access the context. The `CatProvider` component is responsible for fetching the cat data from an API and managing the state of `cats` and `currentCat`.

### Using the Context in Components

Once the context is created, we can use it in our components to access the state and update it as needed. For instance, in the `CatList` component, we can access the list of cats and the current selected cat:

```tsx
// components/CatList.tsx
import React from 'react';
import { useCatContext } from '../context/CatContext';
import CatCard from './CatCard';

const CatList: React.FC = () => {
  const { cats, currentCat, setCurrentCat } = useCatContext();

  const handleCatClick = (cat: Cat) => {
    setCurrentCat(cat);
  };

  return (
    <div className="cat-list">
      {cats.map((cat) => (
        <CatCard key={cat.id} cat={cat} onClick={handleCatClick} />
      ))}
    </div>
  );
};

export default CatList;
```

In this example, the `CatList` component uses the `useCatContext` hook to access the `cats`, `currentCat`, and `setCurrentCat` functions. The `handleCatClick` function is defined to update the `currentCat` state when a cat is clicked. This allows the `CatCard` component to trigger a state update when the user interacts with it.

### Updating the Cat Card Component

To make the `CatCard` component interactive, we need to pass the `onClick` handler to it. Here's how you can modify the `CatCard` component to accept the `onClick` prop:

```tsx
// components/CatCard.tsx
import React from 'react';
import { useCatContext } from '../context/CatContext';

interface CatProps {
  cat: Cat;
  onClick: (cat: Cat) => void;
}

const CatCard: React.FC<CatProps> = ({ cat, onClick }) => {
  const { currentCat } = useCatContext();

  return (
    <div className={`cat-card ${currentCat?.id === cat.id ? 'selected' : ''}`} onClick={() => onClick(cat)}>
      <img src={cat.imageUrl} alt={cat.name} className="cat-image" />
      <h2 className="cat-name">{cat.name}</h2>
      <p className="cat-description">{cat.description}</p>
    </div>
  );
};

export default CatCard;
```

In this updated `CatCard` component, we define the `CatProps` interface to include the `onClick` function. The component uses the `useCatContext` hook to access the `currentCat` state and applies a `selected` class if the current cat matches the one being displayed. This visual feedback helps users understand which cat is currently selected.

### Styling the Selected Cat

To enhance the user experience, we can add some styling to the selected cat card. Here's an example of how to style the selected cat:

```css
/* components/CatCard.css */
.cat-card {
  background-color: #fff;
  border: 2px solid #f9d949;
  border-radius: 10px;
  width: 200px;
  padding: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
  text-align: center;
  cursor: pointer;
}

.cat-card:hover {
  transform: scale(1.05);
}

.cat-card.selected {
  border-color: #ff4d4d;
  box-shadow: 0 4px 8px rgba(255, 0, 0, 0.3);
}
```

This CSS code adds a `cursor: pointer` to the `cat-card` class, indicating that it is clickable. When a cat is selected, the `selected` class changes the border color and adds a more prominent shadow, providing visual feedback to the user.

### Managing State Updates

As the user interacts with the Cat App, it's essential to manage state updates effectively. The React Context API allows for centralized state management, making it easier to update and access the state from any component. For example, when a user selects a cat, the `currentCat` state is updated, and this change is reflected in all components that consume the context.

### Conclusion

By implementing state management using the React Context API, you can create a more cohesive and interactive experience for users of the Cat App. The ability to share and update state across components simplifies the development process and enhances the user interface. The code examples provided demonstrate how to create the context, use it in components, and manage state updates effectively. As you continue to develop the Cat App, consider adding more features that leverage the context for state management, such as saving favorite cats or tracking user interactions. This approach will ensure that your application remains scalable and maintainable as it grows. 😊

## Implementing Routing in the Cat App

In the Cat App, implementing routing is essential for allowing users to navigate between different pages, such as the home page and individual cat profiles. React Router is a powerful library that enables this functionality, making it easy to manage navigation and URL changes in a React application. In this section, we will guide you through the process of setting up React Router, creating routes for the home page and cat detail page, and implementing navigation between them.

### Installing React Router

To begin, you need to install React Router in your project. If you haven't already done so, you can install it using npm or yarn. Run the following command in your terminal:

```bash
npm install react-router-dom
```

Once installed, you can import the necessary components from `react-router-dom` into your application.

### Setting Up the Router

The first step in implementing routing is to set up the `BrowserRouter` in your main application component. This component wraps your entire app and allows for routing. Here's how you can modify your `App.tsx` file to include the router:

```tsx
// App.tsx
import React from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Header from './components/Header';
import HomePage from './pages/HomePage';
import CatDetailPage from './pages/CatDetailPage';

const App: React.FC = () => {
  return (
    <Router>
      <Header />
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/cat/:id" element={<CatDetailPage />} />
      </Routes>
    </Router>
  );
};

export default App;
```

In this code, we import `BrowserRouter`, `Route`, and `Routes` from `react-router-dom`. The `Router` component wraps the `Header` and the `Routes` component, which defines the different routes for our application. The `Route` for the home page is set to the root path (`"/"`), and the route for the cat detail page is set to `"/cat/:id"`, where `:id` is a dynamic parameter representing the cat's unique identifier.

### Creating the Home Page

The home page will display a list of cats. We can create a `HomePage` component that utilizes the `useNavigate` hook to navigate to the cat detail page when a cat is clicked. Here's an example implementation:

```tsx
// pages/HomePage.tsx
import React from