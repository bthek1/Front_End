# Webpack

Webpack is a popular **module bundler** for modern JavaScript applications. It takes your code and dependencies (e.g., JavaScript, CSS, images, etc.), processes them, and bundles them into one or more optimized files that can be served to a browser.

Author

Benedict Thekkel

## Getting started

### Install npm

    sudo apt install npm

### Check

    node -v
    npm -v

### Initialize npm

    npm init -y

### Install Webpack and Loaders

    npm install --save-dev webpack webpack-cli webpack-dev-server
    npm install --save-dev ts-loader css-loader style-loader sass sass-loader
    npm install --save-dev html-webpack-plugin mini-css-extract-plugin

    npm install --save bootstrap sass typescript webpack webpack-cli webpack-dev-server ts-loader css-loader style-loader mini-css-extract-plugin html-webpack-plugin axios

------------------------------------------------------------------------

## **1. What is Webpack?**

Webpack is a tool that: - Bundles JavaScript files into a single file (or multiple files). - Transforms and optimizes other assets (CSS, images, fonts, etc.) into formats browsers can use. - Supports advanced features like code splitting, tree-shaking, and lazy loading.

------------------------------------------------------------------------

## **2. Key Features**

### **a) Module Bundling**

- Webpack treats everything in your project as a module (JavaScript, CSS, images, etc.).
- Supports ES Modules (`import/export`) and CommonJS (`require`).

### **b) Loaders**

- Loaders transform files into modules (e.g., convert SCSS to CSS or TypeScript to JavaScript).
- Examples:

&nbsp;

      - babel loader: Transpiles modern JavaScript (ES6+) to browser-compatible JavaScript.
      - css loader: Enables importing CSS in JavaScript.

### **c) Plugins**

- Plugins extend Webpack’s functionality (e.g., HTML generation, code optimization).
- Examples:

&nbsp;

      - html-webpack-plugin: Injects bundled JavaScript into an HTML template.
      - terser-webpack-plugin: Optimizes and minifies JavaScript.

### **d) Code Splitting**

- Splits your code into smaller chunks to reduce the size of JavaScript files and improve load times.

### **e) Tree Shaking**

- Removes unused code from your final bundle using ES6 module syntax.

### **f) Hot Module Replacement (HMR)**

- Enables live updating of modules in the browser without a full reload.

------------------------------------------------------------------------

## **3. How Webpack Works**

### **a) Entry**

The starting point of your application. Webpack begins building the dependency graph from here.

Example:

``` javascript
module.exports = {
  entry: './src/index.js',
};
```

### **b) Output**

Specifies the location and name of the bundled files.

Example:

``` javascript
module.exports = {
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
};
```

### **c) Loaders**

Process non-JavaScript files (e.g., CSS, images, TypeScript).

Example:

``` javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,  // Matches .css files
        use: ['style-loader', 'css-loader'], // Processes CSS
      },
    ],
  },
};
```

### **d) Plugins**

Extend Webpack’s functionality (e.g., optimization, asset management).

Example:

``` javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
};
```

### **e) Mode**

Defines the environment: - **`development`**: Focuses on fast builds and debugging (includes source maps). - **`production`**: Optimizes the output for performance.

Example:

``` javascript
module.exports = {
  mode: 'production', // or 'development'
};
```

------------------------------------------------------------------------

## **4. Installation and Setup**

### **a) Install Webpack**

1.  Install Webpack and Webpack CLI:

    ``` bash
    npm install webpack webpack-cli --save-dev
    ```

2.  Create a Webpack configuration file (`webpack.config.js`):

    ``` javascript
    const path = require('path');

    module.exports = {
      entry: './src/index.js',
      output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js',
      },
    };
    ```

3.  Add scripts to `package.json`:

    ``` json
    "scripts": {
      "build": "webpack"
    }
    ```

4.  Run Webpack:

    ``` bash
    npm run build
    ```

### **b) Install Loaders**

Install loaders to handle CSS, images, etc.:

``` bash
npm install style-loader css-loader --save-dev
```

Add to `webpack.config.js`:

``` javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
};
```

------------------------------------------------------------------------

## **5. Advanced Features**

### **a) Code Splitting**

Split code into separate files for better performance. Example using dynamic imports:

``` javascript
import('./module.js').then((module) => {
  module.default();
});
```

### **b) Tree Shaking**

Remove unused code:

``` javascript
module.exports = {
  mode: 'production',
};
```

### **c) Lazy Loading**

Load parts of your app on demand:

``` javascript
const button = document.getElementById('myButton');
button.addEventListener('click', () => {
  import('./myModule.js').then((module) => {
    module.doSomething();
  });
});
```

### **d) Dev Server**

Use `webpack-dev-server` for live reloading during development: 1. Install: `bash npm install webpack-dev-server --save-dev`

2.  Add to `webpack.config.js`:

    ``` javascript
    devServer: {
      contentBase: './dist',
      hot: true,
    },
    ```

3.  Run:

    ``` bash
    npx webpack serve
    ```

------------------------------------------------------------------------

## **6. Popular Plugins**

- **`html-webpack-plugin`**: Automatically generates an HTML file with the correct script tags.
- **`mini-css-extract-plugin`**: Extracts CSS into separate files.
- **`clean-webpack-plugin`**: Cleans the `dist` folder before each build.
- **`terser-webpack-plugin`**: Minifies JavaScript files.
- **`copy-webpack-plugin`**: Copies files to the `dist` folder.

------------------------------------------------------------------------

## **7. Example Configuration**

Here’s a complete `webpack.config.js` for a basic project:

``` javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|jpg|gif)$/,
        type: 'asset/resource',
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  mode: 'development',
  devServer: {
    static: './dist',
    hot: true,
  },
};
```

------------------------------------------------------------------------

## **8. Alternatives to Webpack**

While Webpack is powerful, there are alternatives for specific needs: - **Vite**: Focused on fast builds and simplicity. - **Rollup**: Ideal for library bundling. - **Parcel**: Zero-config bundler with simpler defaults. - **Esbuild**: Extremely fast bundler optimized for performance.

------------------------------------------------------------------------

## **9. Pros and Cons**

### **Pros**

- Highly configurable for complex projects.
- Supports advanced features like HMR and tree-shaking.
- Large ecosystem of plugins and loaders.

### **Cons**

- Can be overwhelming for beginners.
- Configuration can become verbose for simple projects.

------------------------------------------------------------------------

## **10. Resources**

- [Official Webpack Documentation](https://webpack.js.org/)
- [Webpack Academy](https://webpack.academy/)
- [Webpack GitHub Repository](https://github.com/webpack/webpack)

------------------------------------------------------------------------

Webpack is a versatile tool that can handle complex dependency graphs, optimize assets, and improve performance. While it has a learning curve, mastering Webpack provides significant benefits for managing modern web projects efficiently.

------------------------------------------------------------------------

Back to top
