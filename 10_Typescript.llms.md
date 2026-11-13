# Typescript

TypeScript is a statically typed superset of JavaScript developed by Microsoft that adds optional static typing to the language. It compiles to plain JavaScript, making it highly versatile for both client-side and server-side applications. Below is everything you need to know about TypeScript:

Author

Benedict Thekkel

## **1. What is TypeScript?**

- **Superset of JavaScript**: TypeScript includes all JavaScript features and adds static typing, interfaces, and advanced tooling support.
- **Type Safety**: Allows you to catch type-related errors at compile time rather than runtime.
- **Compiles to JavaScript**: TypeScript code is transpiled to JavaScript, ensuring compatibility with browsers and JavaScript environments.
- **Used for Large-Scale Projects**: Great for large, complex projects with multiple developers, as it provides better maintainability and readability.

------------------------------------------------------------------------

## **2. Key Features**

1.  **Static Typing**: Adds types to variables, functions, and objects.

    ``` typescript
    let message: string = "Hello, TypeScript!";
    let count: number = 42;
    ```

2.  **Type Inference**: Automatically infers types when they are not explicitly declared.

    ``` typescript
    let inferred = "This is inferred as a string";
    ```

3.  **Interfaces**: Defines the structure of objects, ensuring consistency.

    ``` typescript
    interface User {
        id: number;
        name: string;
    }
    ```

4.  **Enums**: Defines a set of named constants.

    ``` typescript
    enum Direction {
        North,
        South,
        East,
        West,
    }
    ```

5.  **Union Types**: A variable can have multiple types.

    ``` typescript
    let value: string | number;
    value = "Hello";  // Valid
    value = 42;       // Valid
    ```

6.  **Generics**: Enables reusable, type-safe components.

    ``` typescript
    function identity<T>(value: T): T {
        return value;
    }
    ```

7.  **Decorators** (Experimental): Adds metadata to classes and members, often used in frameworks like Angular.

    ``` typescript
    @Component({...})
    class MyComponent {}
    ```

8.  **Modules**: Supports `ES6` modules for importing and exporting code.

    ``` typescript
    import { myFunction } from './myModule';
    export function myFunction() {}
    ```

9.  **Strict Null Checks**: Ensures variables are not `null` or `undefined` unless explicitly allowed.

10. **Advanced Tooling**: Better IntelliSense, autocomplete, and refactoring support in IDEs like Visual Studio Code.

------------------------------------------------------------------------

## **3. Installation**

Install TypeScript globally via npm:

``` bash
npm install -g typescript
```

Check the installed version:

``` bash
tsc --version
```

------------------------------------------------------------------------

## **4. Setting Up a TypeScript Project**

### **a. Initialize a New Project**

1.  Create a new directory:

    ``` bash
    mkdir my-project && cd my-project
    ```

2.  Initialize `package.json`:

    ``` bash
    npm init -y
    ```

3.  Install TypeScript locally:

    ``` bash
    npm install typescript --save-dev
    ```

4.  Create a `tsconfig.json`:

    ``` bash
    npx tsc --init
    ```

------------------------------------------------------------------------

### **b. Example `tsconfig.json`**

``` json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "ES6",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "resolveJsonModule": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

## **5. Compiling TypeScript**

Compile `.ts` files to `.js`:

``` bash
npx tsc
```

You can also compile a single file:

``` bash
npx tsc file.ts
```

Run the JavaScript file:

``` bash
node dist/file.js
```

------------------------------------------------------------------------

## **6. TypeScript vs JavaScript**

| Feature | **TypeScript** | **JavaScript** |
|----|----|----|
| **Typing** | Statically typed (type checking at compile time). | Dynamically typed. |
| **Error Detection** | Compile-time errors for type mismatches. | Errors detected at runtime. |
| **Tooling** | Superior tooling and editor support. | Limited tooling capabilities. |
| **Backward Compatibility** | Compiles to ES3+ JavaScript for compatibility. | Runs directly in browsers or Node.js. |

------------------------------------------------------------------------

## **7. Advanced Features**

### **a. Type Aliases**

Alias complex types for readability:

``` typescript
type Point = { x: number; y: number };
let pt: Point = { x: 10, y: 20 };
```

### **b. Intersection Types**

Combine multiple types:

``` typescript
type Admin = { id: number; role: string };
type User = { name: string };
type AdminUser = Admin & User;
```

### **c. Utility Types**

TypeScript includes built-in utility types like `Pick`, `Partial`, and `Omit`:

``` typescript
interface User {
    id: number;
    name: string;
    email: string;
}
type PartialUser = Partial<User>; // All properties are optional
type PickedUser = Pick<User, "id" | "email">;
```

### **d. Type Guards**

Refine types at runtime:

``` typescript
function isString(value: unknown): value is string {
    return typeof value === 'string';
}
```

------------------------------------------------------------------------

## **8. TypeScript with Frameworks**

### **a. React**

Install TypeScript for React:

``` bash
npx create-react-app my-app --template typescript
```

Use `.tsx` for TypeScript files with JSX.

### **b. Node.js**

Install TypeScript for Node.js:

``` bash
npm install @types/node --save-dev
```

### **c. Angular**

Angular uses TypeScript by default.

------------------------------------------------------------------------

## **9. Integrating TypeScript into Existing Projects**

1.  Add TypeScript to an existing project:

    ``` bash
    npm install typescript --save-dev
    ```

2.  Rename `.js` files to `.ts` and fix type errors.

3.  Gradually enable strict checks in `tsconfig.json`.

------------------------------------------------------------------------

## **10. TypeScript with Third-Party Libraries**

Install type definitions for popular libraries:

``` bash
npm install @types/lodash --save-dev
```

------------------------------------------------------------------------

## **11. Tooling and Ecosystem**

- **Editors**: Works best with Visual Studio Code.
- **Linting**: Use ESLint with TypeScript.
- **Testing**: Use frameworks like Jest or Mocha with TypeScript.

------------------------------------------------------------------------

## **12. Advantages of TypeScript**

1.  **Improved Code Quality**: Early detection of bugs through static typing.
2.  **Refactoring Support**: Easier to refactor large codebases with type safety.
3.  **Tooling**: Enhanced IntelliSense, auto-completion, and debugging.
4.  **Large Community**: Widespread adoption and support.

------------------------------------------------------------------------

## **13. Disadvantages of TypeScript**

1.  **Learning Curve**: Requires learning types and new syntax.
2.  **Extra Compilation Step**: Must compile `.ts` to `.js`.
3.  **Overhead**: Adds some complexity for small projects.

------------------------------------------------------------------------

## **14. TypeScript vs Other Languages**

| Feature       | TypeScript        | JavaScript | Python  | Java   |
|---------------|-------------------|------------|---------|--------|
| Typing        | Static (optional) | Dynamic    | Dynamic | Static |
| Compilation   | Yes               | No         | No      | Yes    |
| Runtime Speed | Fast              | Fast       | Slower  | Fast   |
| Popularity    | Growing           | High       | High    | Stable |

------------------------------------------------------------------------

Back to top
