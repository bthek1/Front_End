# npm

npm (Node Package Manager) is the default package manager for Node.js, and it’s an essential tool for managing JavaScript dependencies and packages. Here’s a comprehensive guide to understanding and using npm.

Author

Benedict Thekkel

## **1. What is npm?**

- **Definition**: npm is a command-line tool and an online repository for managing JavaScript packages.
- **Purpose**:
  - Install, manage, and share JavaScript libraries and frameworks.
  - Manage dependencies for JavaScript projects.
  - Publish and share your own packages.

------------------------------------------------------------------------

## **2. Key Features of npm**

- **Package Management**:
  - Install and manage third-party libraries for your project.
  - Specify project dependencies in `package.json`.
- **Version Control**:
  - Manage package versions using semantic versioning (SemVer).
- **Script Automation**:
  - Use `npm` scripts to automate tasks like testing, building, or running applications.

------------------------------------------------------------------------

## **3. Installing npm**

npm is bundled with Node.js, so installing Node.js will automatically install npm.

- Install Node.js (and npm):

  - **Windows/Mac**: Download from [Node.js official site](https://nodejs.org/).

  - **Linux**: Use a package manager like `nvm` (Node Version Manager).

    ``` bash
    sudo apt install npm
    ```

- Verify installation:

  ``` bash
  node -v   # Check Node.js version
  npm -v    # Check npm version
  ```

------------------------------------------------------------------------

## **4. Key npm Commands**

### **a. Installing Packages**

#### Local Installation (for a specific project):

``` bash
npm install package-name
```

- Installs the package in the `node_modules` directory.
- Updates `dependencies` in `package.json`.

#### Global Installation (for CLI tools):

``` bash
npm install -g package-name
```

- Installs the package globally, making it available system-wide.

#### Installing Specific Versions:

``` bash
npm install package-name@version
```

#### Development Dependencies:

``` bash
npm install package-name --save-dev
```

- Adds the package under `devDependencies` in `package.json`.

------------------------------------------------------------------------

### **b. Removing Packages**

``` bash
npm uninstall package-name
```

- Removes the package from `node_modules` and `package.json`.

------------------------------------------------------------------------

### **c. Listing Installed Packages**

``` bash
npm list       # Lists locally installed packages
npm list -g    # Lists globally installed packages
```

------------------------------------------------------------------------

### **d. Initializing a New Project**

``` bash
npm init       # Interactive setup
npm init -y    # Automatically generate a `package.json` with defaults
```

------------------------------------------------------------------------

### **e. Updating Packages**

Update all dependencies to their latest compatible versions:

``` bash
npm update
```

Update a specific package:

``` bash
npm install package-name@latest
```

To upgrade all packages to their latest versions:

``` bash
npx npm-check-updates -u
npm install
```

------------------------------------------------------------------------

### **f. Running npm Scripts**

Scripts defined in `package.json` can be run using:

``` bash
npm run script-name
```

Example:

``` json
"scripts": {
  "start": "node app.js",
  "build": "webpack --config webpack.config.js",
  "test": "jest"
}
```

Run the `start` script:

``` bash
npm start
```

------------------------------------------------------------------------

## **5. Understanding `package.json`**

`package.json` is a metadata file that describes your project and its dependencies.

### Key Fields:

- **`name`**: Project name.
- **`version`**: Current version of the project.
- **`dependencies`**: Lists runtime dependencies.
- **`devDependencies`**: Lists development-only dependencies.
- **`scripts`**: Defines npm scripts for automating tasks.

Example:

``` json
{
  "name": "my-project",
  "version": "1.0.0",
  "scripts": {
    "start": "node app.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "jest": "^27.0.6"
  }
}
```

------------------------------------------------------------------------

## **6. npm Cache**

npm uses a cache to store downloaded packages for faster re-installation.

- Clear the cache:

``` bash
npm cache clean --force
```

------------------------------------------------------------------------

## **7. Versioning in npm**

npm uses **Semantic Versioning** (SemVer): - **`^1.2.3`**: Allows updates that do not change the major version (e.g., `1.x.x`). - **`~1.2.3`**: Allows updates that do not change the minor version (e.g., `1.2.x`). - **`1.2.3`**: Installs the exact version.

------------------------------------------------------------------------

## **8. Using `.npmrc`**

Customize npm behavior with the `.npmrc` file: - Set a registry: `bash registry=https://registry.npmjs.org/` - Use a proxy: `bash proxy=http://proxy.example.com:8080`

------------------------------------------------------------------------

## **9. npm Registry**

The npm registry is a public database of JavaScript packages.

- Browse packages on [npmjs.com](https://www.npmjs.com/).

- Publish your own package:

  ``` bash
  npm publish
  ```

------------------------------------------------------------------------

## **10. Common Issues and Fixes**

#### **a. Permission Errors**

Use `nvm` to manage Node.js versions and avoid using `sudo` with npm:

``` bash
nvm use stable
```

#### **b. Outdated npm**

Update npm to the latest version:

``` bash
npm install -g npm
```

------------------------------------------------------------------------

## **11. Best Practices**

1.  **Use `package-lock.json`**:
    - Ensures consistent dependency versions across environments.
2.  **Use `.gitignore`**:
    - Exclude `node_modules` from version control.
3.  **Use Semantic Versioning**:
    - Maintain backward compatibility with `^` or `~`.
4.  **Automate with Scripts**:
    - Simplify tasks like builds and testing with npm scripts.

------------------------------------------------------------------------

## **12. Ecosystem**

- **Popular npm Libraries**:
  - `express`: Web framework.
  - `react`: Front-end library.
  - `lodash`: Utility functions.
  - `axios`: HTTP client.
  - `jest`: Testing framework.
- **Build Tools**:
  - `webpack`: Asset bundler.
  - `parcel`: Zero-config bundler.
  - `vite`: Modern build tool.

------------------------------------------------------------------------

## **13. Alternatives to npm**

- **Yarn**: A faster, more secure package manager.
- **pnpm**: Focuses on performance and efficient storage.

------------------------------------------------------------------------

Back to top
