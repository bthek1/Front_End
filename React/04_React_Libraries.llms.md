# React Libraries

Here’s a curated list of **popular and essential npm add-ons for React projects**, organized by category, including their purpose, popularity, and common use cases.

Author

Benedict Thekkel

------------------------------------------------------------------------

## 📦 1. **Routing & Navigation**

| Package | Use Case |
|----|----|
| `react-router-dom` | Declarative routing (SPA, nested routes, lazy loading) |
| `@tanstack/react-router` | Advanced router with data loading, similar to Remix/Next.js |

``` bash
npm install react-router-dom
```

------------------------------------------------------------------------

## 🌍 2. **Global State Management**

| Package | Description |
|----|----|
| `zustand` | Simple, scalable state with hooks (minimal Redux alternative) |
| `redux` + `react-redux` | Predictable state container (more boilerplate) |
| `jotai` | Primitive and minimal atomic state |
| `recoil` | State management by Meta (atom/selectors model) |

``` bash
npm install zustand
```

------------------------------------------------------------------------

## 🔌 3. **Data Fetching / Caching**

| Package | Description |
|----|----|
| `@tanstack/react-query` (React Query) | Caching, revalidation, pagination |
| `swr` | Lightweight data-fetching library by Vercel |

``` bash
npm install @tanstack/react-query
```

------------------------------------------------------------------------

## 🎨 4. **Styling**

| Package             | Description                        |
|---------------------|------------------------------------|
| `tailwindcss`       | Utility-first CSS framework        |
| `styled-components` | CSS-in-JS styling                  |
| `@emotion/react`    | Another powerful CSS-in-JS library |
| `classnames`        | Conditionally join classNames      |

``` bash
npm install tailwindcss classnames
```

------------------------------------------------------------------------

## 🧪 5. **Testing**

| Package                  | Description                   |
|--------------------------|-------------------------------|
| `@testing-library/react` | Test components like users do |
| `jest` / `vitest`        | Test runners                  |
| `cypress` / `playwright` | E2E browser testing           |

``` bash
npm install --save-dev @testing-library/react vitest
```

------------------------------------------------------------------------

## 🎭 6. **Form Handling & Validation**

| Package           | Description                         |
|-------------------|-------------------------------------|
| `react-hook-form` | Performant, minimal form management |
| `formik`          | Traditional form state management   |
| `zod` / `yup`     | Schema validation libraries         |

``` bash
npm install react-hook-form zod
```

------------------------------------------------------------------------

## 🧱 7. **UI Components / Design Systems**

| Package            | Description                              |
|--------------------|------------------------------------------|
| `@mui/material`    | Google’s Material UI                     |
| `@chakra-ui/react` | Accessible, composable component library |
| `shadcn/ui`        | Modern, headless + Tailwind components   |
| `antd`             | Enterprise-grade components (Ant Design) |

``` bash
npm install @mui/material @emotion/react @emotion/styled
```

------------------------------------------------------------------------

## 📊 8. **Charts & Visualization**

| Package                        | Description                     |
|--------------------------------|---------------------------------|
| `recharts`                     | Composable chart components     |
| `chart.js` + `react-chartjs-2` | Popular canvas-based charting   |
| `plotly.js`                    | Interactive and powerful charts |

``` bash
npm install recharts
```

------------------------------------------------------------------------

## 🔧 9. **Dev Tools & Productivity**

| Package               | Description                 |
|-----------------------|-----------------------------|
| `eslint` + `prettier` | Code quality and formatting |
| `vite-plugin-eslint`  | Live linting in Vite        |
| `eslint-plugin-react` | React-specific lint rules   |
| `typescript`          | Optional static typing      |

``` bash
npm install -D eslint prettier eslint-plugin-react
```

------------------------------------------------------------------------

## 🧠 10. **AI & LLM Integration**

| Package                | Description                                        |
|------------------------|----------------------------------------------------|
| `langchain`            | Chain logic and prompts for LLMs                   |
| `openai`               | Direct API client to OpenAI                        |
| `@xenova/transformers` | Transformers.js inference in browser (LLM locally) |

``` bash
npm install openai
```

------------------------------------------------------------------------

## 🔌 11. **Other Handy Utilities**

| Package               | Use                        |
|-----------------------|----------------------------|
| `axios`               | HTTP client                |
| `dayjs` or `date-fns` | Date manipulation          |
| `uuid`                | Generate UUIDs             |
| `dotenv`              | Load environment variables |

``` bash
npm install axios dayjs uuid
```

------------------------------------------------------------------------

## 📘 Summary Table

| Category      | Must-Have Addons                                 |
|---------------|--------------------------------------------------|
| Routing       | `react-router-dom`                               |
| State         | `zustand`, `redux`, `jotai`                      |
| Data Fetching | `@tanstack/react-query`, `swr`                   |
| Styling       | `tailwindcss`, `styled-components`, `classnames` |
| Forms         | `react-hook-form`, `zod`                         |
| UI Components | `@mui/material`, `shadcn/ui`, `chakra-ui`        |
| Testing       | `@testing-library/react`, `vitest`               |
| Charts        | `recharts`, `chart.js`, `plotly.js`              |
| Utils         | `axios`, `uuid`, `dayjs`                         |

------------------------------------------------------------------------

Back to top
