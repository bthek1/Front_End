# Prettier

**Prettier** is a popular opinionated code formatter for multiple programming languages, including JavaScript, TypeScript, HTML, CSS, JSON, and more. It enforces consistent style rules across your codebase by formatting your code to follow a single, uniform standard.

Author

Benedict Thekkel

## **1. Key Features of Prettier**

- **Opinionated**: Prettier enforces a consistent code style with minimal configuration.
- **Language Support**: Supports a wide range of languages, including JavaScript, TypeScript, HTML, CSS, SCSS, JSON, YAML, Markdown, and more.
- **Automatic Formatting**: Formats code automatically, eliminating manual adjustments.
- **No Debates**: Reduces arguments about formatting styles in teams.
- **Extensible**: Supports custom configurations for specific rules (e.g., line width, quote style).
- **Integrations**: Compatible with many editors, pre-commit hooks, and CI pipelines.

------------------------------------------------------------------------

## **2. Installation**

### **Install Globally**

Install Prettier globally using npm:

``` bash
npm install -g prettier
```

### **Install Locally (Recommended for Projects)**

Install Prettier as a development dependency in your project:

``` bash
npm install --save-dev prettier
```

------------------------------------------------------------------------

## **3. Basic Usage**

### **Command-Line Interface (CLI)**

1.  **Format a File**:

    ``` bash
    prettier --write file.js
    ```

2.  **Check Formatting** (without applying changes):

    ``` bash
    prettier --check file.js
    ```

3.  **Format All Files in a Project**:

    ``` bash
    prettier --write .
    ```

4.  **Specify File Types**:

    ``` bash
    prettier --write "**/*.js"
    ```

------------------------------------------------------------------------

## **4. Configuration**

### **Prettier Configuration File**

Prettier can be configured using a variety of file types. Create a configuration file in your project root:

- `.prettierrc`
- `.prettierrc.json`
- `.prettierrc.yaml`
- `.prettierrc.js`

### **Example Configuration (`.prettierrc`)**

``` json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "useTabs": false,
  "trailingComma": "es5",
  "printWidth": 80,
  "bracketSpacing": true
}
```

### **Key Options:**

| Option           | Default | Description                                     |
|------------------|---------|-------------------------------------------------|
| `semi`           | `true`  | Adds semicolons at the end of statements.       |
| `singleQuote`    | `false` | Use single quotes instead of double quotes.     |
| `tabWidth`       | `2`     | Number of spaces per tab.                       |
| `useTabs`        | `false` | Use tabs instead of spaces for indentation.     |
| `trailingComma`  | `"es5"` | Add trailing commas where valid in ES5.         |
| `printWidth`     | `80`    | Max line width before wrapping.                 |
| `bracketSpacing` | `true`  | Add spaces between brackets in object literals. |

------------------------------------------------------------------------

### **Ignore Files**

Prettier can ignore specific files using a `.prettierignore` file:

    node_modules/
    dist/
    build/
    *.min.js

------------------------------------------------------------------------

## **5. Prettier in VS Code**

### **Extension**

Install the official **Prettier - Code Formatter** extension in VS Code.

1.  **Open Extensions Marketplace**: `Ctrl+Shift+X` or `Cmd+Shift+X`.
2.  Search for “Prettier - Code Formatter.”
3.  Click **Install**.

### **Configuration in VS Code**

Add the following to your `settings.json`:

``` json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  "prettier.tabWidth": 4,
  "prettier.singleQuote": true,
  "prettier.semi": false
}
```

------------------------------------------------------------------------

## **6. Integration with ESLint**

Prettier can be integrated with ESLint to handle both linting and formatting.

1.  **Install ESLint and Prettier Plugins**:

    ``` bash
    npm install --save-dev eslint prettier eslint-plugin-prettier eslint-config-prettier
    ```

2.  **Update `.eslintrc`**:

    ``` json
    {
      "extends": [
        "eslint:recommended",
        "plugin:prettier/recommended"
      ],
      "rules": {
        "prettier/prettier": [
          "error",
          {
            "singleQuote": true,
            "semi": false
          }
        ]
      }
    }
    ```

3.  **Run Both**:

    ``` bash
    eslint --fix .
    prettier --write .
    ```

------------------------------------------------------------------------

## **7. Pre-commit Hook with Prettier**

Use **pre-commit hooks** to format code before committing:

1.  **Install `husky` and `lint-staged`**:

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
        "**/*.{js,ts,json,css,md}": [
          "prettier --write",
          "git add"
        ]
      }
    }
    ```

3.  **Activate Husky**:

    ``` bash
    npx husky install
    ```

------------------------------------------------------------------------

## **8. Supported Languages**

Prettier supports the following file types:

- **JavaScript & TypeScript**: `.js`, `.jsx`, `.ts`, `.tsx`
- **HTML**: `.html`, `.htm`
- **CSS & SCSS**: `.css`, `.scss`, `.less`
- **JSON & YAML**: `.json`, `.yaml`, `.yml`
- **Markdown**: `.md`
- **Other**: `.vue`, `.svelte`, `.graphql`

------------------------------------------------------------------------

## **9. Advanced Usage**

### **Custom Parsers**

Prettier supports custom parsers for non-standard file types. For example, to use a custom Markdown parser:

``` bash
prettier --parser markdown file.md
```

### **CLI Options**

Run `prettier --help` to see all available options. Examples:

- Check specific files:

  ``` bash
  prettier --check "src/**/*.js"
  ```

- Write formatted output to a new file:

  ``` bash
  prettier file.js > formatted.js
  ```

------------------------------------------------------------------------

## **10. Best Practices**

1.  **Format-on-Save**: Enable auto-formatting in your editor for faster feedback.
2.  **Consistent Config**: Share a `.prettierrc` file across your project.
3.  **Pair with ESLint**: Use Prettier with ESLint for both formatting and linting.
4.  **Pre-commit Hook**: Prevent unformatted code from being committed.

------------------------------------------------------------------------

## **11. Alternatives to Prettier**

- **ESLint**: Primarily a linter but can be used for formatting with plugins.
- **StandardJS**: Linter and formatter with its own set of rules.
- **Beautify**: A highly customizable code formatter for various languages.

------------------------------------------------------------------------

**Prettier** simplifies code formatting, increases readability, and improves consistency across your projects. Its integration with editors, CI/CD pipelines, and linting tools makes it a must-have for modern development workflows.

------------------------------------------------------------------------

Back to top
