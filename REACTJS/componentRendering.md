# Loading componets in react

- To load a component in React, you must first export it from its own file, import it into the parent component,
- Then render it using JSX. 

## There are also techniques for loading components conditionally or on demand, 

- which is useful for single-page applications and performance optimization. 
Standard component loading

### **Step 1:** Create and export a component

Create a new file for your component (e.g., MyComponent.jsx). Define a functional component and use export default to make it available for other files to import. 
MyComponent.jsx
javascript

```jsx
// A simple functional component
function MyComponent() {
  return (
    <div>
      <h1>Hello from My Component!</h1>
      <p>This is a separate, reusable component.</p>
    </div>
  );
}

// Export the component to be used elsewhere
export default MyComponent;
```

### **Step 2:** Import the component

In the file where you want to use your component (e.g., App.jsx), use an import statement at the top of the file to bring it in. 

App.jsx
javascript

```jsx
// Import MyComponent from its file
import MyComponent from './MyComponent.jsx';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1>My React Page</h1>
      </header>
    </div>
  );
}

export default App;
```

### **Step 3:** Render the component with JSX

Inside the return statement of your App component, use the imported component's name as a JSX tag to render it. 

App.jsx

javascript

```jsx
import MyComponent from './MyComponent.jsx';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1>My React Page</h1>
        {/* Render the component here */}
        <MyComponent />
      </header>
    </div>
  );
}

export default App;
```
---

## Conditional loading based on a button click

You can use state to control whether a component is visible or not. This is a common pattern for showing and hiding information, like a modal or a details panel. 

javascript

```jsx
import React, { useState } from 'react';
import MyComponent from './MyComponent.jsx';

function App() {
  // Use state to track if the component should be shown
  const [isComponentVisible, setIsComponentVisible] = useState(false);

  const toggleVisibility = () => {
    setIsComponentVisible(!isComponentVisible);
  };

  return (
    <div>
      <button onClick={toggleVisibility}>
        {isComponentVisible ? 'Hide Component' : 'Show Component'}
      </button>

      {/* Conditionally render MyComponent */}
      {isComponentVisible && <MyComponent />}
    </div>
  );
}

export default App;
```

## Advanced loading with React Router

For single-page applications with different "pages," you can load components by using a routing library like React Router. This allows you to render a different component based on the URL in the browser's address bar. 

- **Install React Router:** Run npm install react-router-dom in your project's terminal.
Set up routing in App.jsx: 

App.jsx

javascript

```jsx
import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>
      <Routes>
        {/* Load the Home component when the URL is "/" */}
        <Route path="/" element={<Home />} />
        {/* Load the About component when the URL is "/about" */}
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}

export default App;
```

## On-demand or "lazy" loading

For large applications, lazy loading can improve performance by only loading a component's code when it is actually needed, rather than all at once when the page loads. This is done using React.lazy() and <Suspense>. 

```bash
Home.jsx
```

javascript

```jsx
import React, { lazy, Suspense } from 'react';

// Use React.lazy() to dynamically import the component
const HeavyComponent = lazy(() => import('./HeavyComponent'));

function Home() {
  return (
    <div>
      <h1>Home Page</h1>
      {/* Use Suspense to show a fallback while the component loads */}
      <Suspense fallback={<div>Loading...</div>}>
        <HeavyComponent />
      </Suspense>
    </div>
  );
}

export default Home;
```

### HeavyComponent.jsx

javascript

```jsx
// This component will only be loaded when Home renders
function HeavyComponent() {
  return <p>This is a heavy component that loaded on demand!</p>;
}

export default HeavyComponent;
```
