# React Setup

Javascript App development

Author

Benedict Thekkel

------------------------------------------------------------------------

## 🚀 1. **Quick Setup (Vite + React + TypeScript)**

### 📦 Installation

``` bash
# Create project
npm create vite@latest my-app -- --template react-ts

# Move into project
cd my-app

# Install dependencies
npm install

# Start dev server
npm run dev
```

------------------------------------------------------------------------

## 🗂️ 2. **Project Structure Explained**

    my-app/
    ├── public/               # Static assets (favicon, robots.txt)
    │   └── vite.svg
    ├── src/                  # All source code lives here
    │   ├── assets/           # Images, fonts, etc.
    │   ├── components/       # Reusable UI components
    │   │   └── Button.tsx
    │   ├── pages/            # Pages for routes (e.g., Home, About)
    │   │   └── Home.tsx
    │   ├── hooks/            # Custom React hooks
    │   ├── styles/           # Global styles (e.g., Tailwind, CSS Modules)
    │   ├── App.tsx           # Root component
    │   ├── main.tsx          # Entry point (ReactDOM.render)
    │   └── types/            # Shared TypeScript types
    ├── .eslintrc.cjs         # Linting rules
    ├── index.html            # HTML template
    ├── package.json          # Project config and dependencies
    ├── tsconfig.json         # TypeScript configuration
    └── vite.config.ts        # Vite config

------------------------------------------------------------------------

## 💡 3. **Core Files & Concepts**

### `main.tsx` — Entry Point

``` tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './styles/global.css'; // if using global styles

ReactDOM.createRoot(document.getElementById('root')!).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### `App.tsx` — Root Component

``` tsx
import React from 'react';
import Home from './pages/Home';

function App() {
  return (
    <div className="App">
      <h1>Welcome to React</h1>
      <Home />
    </div>
  );
}

export default App;
```

------------------------------------------------------------------------

## 🧩 4. **Component Example**

### `components/Button.tsx`

``` tsx
import React from 'react';

type Props = {
  label: string;
  onClick: () => void;
};

const Button: React.FC<Props> = ({ label, onClick }) => (
  <button onClick={onClick} className="btn">
    {label}
  </button>
);

export default Button;
```

------------------------------------------------------------------------

## 🌐 5. **Routing Setup (with `react-router-dom`)**

### 📦 Install

``` bash
npm install react-router-dom
```

### 🛠️ Setup

#### `main.tsx`

``` tsx
import { BrowserRouter } from 'react-router-dom';

ReactDOM.createRoot(document.getElementById('root')!).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

#### `App.tsx`

``` tsx
import { Routes, Route } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
    </Routes>
  );
}
```

------------------------------------------------------------------------

## 🎣 6. **Custom Hook Example**

### `hooks/useCounter.ts`

``` tsx
import { useState } from 'react';

export function useCounter(initial = 0) {
  const [count, setCount] = useState(initial);
  const increment = () => setCount((c) => c + 1);
  const decrement = () => setCount((c) => c - 1);
  return { count, increment, decrement };
}
```

------------------------------------------------------------------------

## 🧪 7. **Testing Setup**

### 📦 Install

``` bash
npm install --save-dev vitest @testing-library/react @testing-library/jest-dom
```

### `Button.test.tsx`

``` tsx
import { render, screen } from '@testing-library/react';
import Button from './Button';

test('renders button with label', () => {
  render(<Button label="Click me" onClick={() => {}} />);
  expect(screen.getByText('Click me')).toBeInTheDocument();
});
```

------------------------------------------------------------------------

## 🧼 8. **Linting + Formatting**

### 📦 Install

``` bash
npm install -D eslint prettier eslint-plugin-react eslint-config-prettier
```

### `.eslintrc.cjs`

``` js
module.exports = {
  extends: ['react-app', 'plugin:react/recommended', 'prettier'],
};
```

------------------------------------------------------------------------

## 🎨 9. **Styling Options**

| Approach          | Tools                           |
|-------------------|---------------------------------|
| Utility-first CSS | Tailwind CSS                    |
| Component-scoped  | CSS Modules / Styled-components |
| Global CSS        | Plain CSS / SCSS                |

``` bash
# Tailwind example setup
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

------------------------------------------------------------------------

## 📦 10. **Helpful Commands**

| Task             | Command                        |
|------------------|--------------------------------|
| Start dev server | `npm run dev`                  |
| Build for prod   | `npm run build`                |
| Preview build    | `npm run preview`              |
| Run tests        | `npx vitest` or `npm run test` |
| Format code      | `npx prettier --write .`       |

------------------------------------------------------------------------

Back to top
