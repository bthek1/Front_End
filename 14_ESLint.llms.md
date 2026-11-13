# ESLint

**ESLint** is a widely used, pluggable, and configurable **linter** for JavaScript and TypeScript. It helps catch errors, enforce consistent coding styles, and integrate with codebases to maintain high-quality code. Below is a comprehensive guide to ESLint.

Author

Benedict Thekkel

## **1. What is ESLint?**

- **Linter**: Identifies problematic patterns in JavaScript/TypeScript code.
- **Customizable**: Allows users to define rules or extend existing configurations.
- **Pluggable**: Supports plugins for additional rules and integration with frameworks.
- **Error Prevention**: Detects errors like unused variables, incorrect syntax, or non-standard coding practices.
- **Code Style Enforcement**: Enforces coding standards for consistency across a project.

------------------------------------------------------------------------

## **2. Key Features**

1.  **Custom Rules**: Define custom linting rules to meet your team’s requirements.
2.  **Plugin Support**: Extend functionality with plugins (e.g., React, TypeScript, Prettier).
3.  **Configurable**: Supports multiple configuration formats (`.eslintrc` files or `package.json`).
4.  **Error Levels**: Classify issues as:
    - `off` → Rule disabled
    - `warn` → Shows a warning
    - `error` → Fails the linting process
5.  **Fixes**: Supports automatic fixing of certain issues via the `--fix` flag.

------------------------------------------------------------------------

## **3. Installation**

### **Install Globally (Optional)**

For global use across projects:

``` bash
npm install -g eslint
```

### **Install Locally (Recommended)**

For project-specific use:

``` bash
npm install eslint --save-dev
```

------------------------------------------------------------------------

## **4. Configuration**

ESLint requires a configuration file to operate. The configuration determines which rules are enabled, disabled, or customized.

### **Common Configuration File Types**

- `.eslintrc.json` (JSON format)
- `.eslintrc.js` (JavaScript format)
- `.eslintrc.yml` (YAML format)
- `package.json` (inside the `eslintConfig` field)

### **Create a Configuration**

You can create an ESLint configuration file interactively:

``` bash
npx eslint --init
```

This command prompts you to choose: 1. **Type of Project** (e.g., Node.js, React). 2. **Language** (JavaScript/TypeScript). 3. **Styling Rules** (e.g., Airbnb, StandardJS, Prettier).

------------------------------------------------------------------------

### **Basic Example Configuration**

#### **`.eslintrc.json`**

``` json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "rules": {
    "no-unused-vars": "warn",
    "eqeqeq": "error",
    "quotes": ["error", "single"]
  }
}
```

#### **Explanation**:

- **`env`**: Defines environments (e.g., browser, Node.js).
- **`extends`**: Extends existing rule sets (e.g., `eslint:recommended`, React rules).
- **`parserOptions`**: Configures ECMAScript version and module type.
- **`rules`**: Overrides or customizes specific rules.

------------------------------------------------------------------------

## **5. Running ESLint**

### **Lint Files**

To lint a specific file:

``` bash
npx eslint file.js
```

### **Lint All Files**

To lint all JavaScript files in the current directory:

``` bash
npx eslint .
```

### **Fix Issues Automatically**

To automatically fix fixable issues:

``` bash
npx eslint . --fix
```

### **Ignore Files**

Create an `.eslintignore` file to specify files or directories to exclude:

    node_modules/
    dist/
    build/

------------------------------------------------------------------------

## **6. Using ESLint with TypeScript**

1.  **Install ESLint and TypeScript Plugins**:

    ``` bash
    npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
    ```

2.  **Update Configuration**:

    ``` json
    {
      "parser": "@typescript-eslint/parser",
      "extends": [
        "eslint:recommended",
        "plugin:@typescript-eslint/recommended"
      ],
      "rules": {
        "@typescript-eslint/no-unused-vars": "warn"
      }
    }
    ```

3.  **Lint TypeScript Files**:

    ``` bash
    npx eslint --ext .ts .
    ```

------------------------------------------------------------------------

## **7. Popular ESLint Plugins**

### **1. React**

- **Plugin**: `eslint-plugin-react`

- **Purpose**: Adds React-specific linting rules.

- **Install**:

  ``` bash
  npm install eslint-plugin-react --save-dev
  ```

### **2. Prettier**

- **Plugin**: `eslint-config-prettier`

- **Purpose**: Disables ESLint rules that conflict with Prettier.

- **Install**:

  ``` bash
  npm install eslint-config-prettier eslint-plugin-prettier --save-dev
  ```

### **3. Import Sorting**

- **Plugin**: `eslint-plugin-import`

- **Purpose**: Enforces import sorting and consistency.

- **Install**:

  ``` bash
  npm install eslint-plugin-import --save-dev
  ```

------------------------------------------------------------------------

## **8. Integrating ESLint with Prettier**

### **Purpose**:

- Use ESLint for linting.
- Use Prettier for formatting.

### **Install Required Packages**:

``` bash
npm install --save-dev eslint prettier eslint-config-prettier eslint-plugin-prettier
```

### **Update Configuration**:

``` json
{
  "extends": [
    "eslint:recommended",
    "plugin:prettier/recommended"
  ],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

### **Run Both**:

``` bash
npx eslint . --fix
npx prettier --write .
```

------------------------------------------------------------------------

## **9. Using ESLint in VS Code**

### **Install ESLint Extension**

- Open VS Code.
- Search for “ESLint” in the Extensions Marketplace.
- Install the **ESLint** extension by Microsoft.

### **Configure VS Code Settings**

Add the following to your **`settings.json`**:

``` json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ]
}
```

### **How It Works**:

- **`source.fixAll.eslint`**: Automatically fixes ESLint issues on save.
- **`eslint.validate`**: Specifies file types for ESLint to validate.

------------------------------------------------------------------------

## **10. Integrating ESLint with Pre-commit Hooks**

Use **Husky** and **lint-staged** to run ESLint before committing code:

1.  **Install Husky and lint-staged**:

    ``` bash
    npm install --save-dev husky lint-staged
    ```

2.  **Update `package.json`**:

    ``` json
    {
      "husky": {
        "hooks": {
          "pre-commit": "lint-staged"
        }
      },
      "lint-staged": {
        "*.js": "eslint --fix"
      }
    }
    ```

3.  **Enable Husky**:

    ``` bash
    npx husky install
    ```

------------------------------------------------------------------------

## **11. Best Practices**

1.  **Use Recommended Configurations**:
    - Start with `eslint:recommended` or other popular presets like Airbnb or Prettier.
2.  **Combine with Prettier**:
    - Use Prettier for formatting and ESLint for linting.
3.  **Integrate with CI/CD**:
    - Add ESLint checks to your CI pipeline to enforce coding standards.
4.  **Custom Rules**:
    - Add rules specific to your project or team’s coding guidelines.

------------------------------------------------------------------------

## **12. Alternatives to ESLint**

- **JSHint**: Earlier tool for linting JavaScript, but lacks modern features.
- **StandardJS**: A zero-config linter with its own style guide.
- **TSLint**: Deprecated, but previously used for TypeScript (replaced by ESLint).

------------------------------------------------------------------------

## **13. Example ESLint Configurations**

### **Airbnb Style Guide**

``` bash
npm install eslint-config-airbnb --save-dev
```

``` json
{
  "extends": ["airbnb"]
}
```

### **Node.js**

``` json
{
  "env": {
    "node": true
  },
  "extends": ["eslint:recommended"]
}
```

------------------------------------------------------------------------

Back to top
