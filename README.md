# data-dashbord
## Setup Steps - From Scratch

These steps outline the process we followed to create this React TypeScript project from the very beginning, troubleshooting included!

1.  **Create the Project Directory:**

    ```
    mkdir data-dashboard
    cd data-dashboard
    ```

2.  **Initialize npm:**

    ```
    npm init -y
    ```

3.  **Install Core Dependencies:**

    ```
    npm install react react-dom typescript @types/react @types/react-dom
    ```

4.  **Install Development Dependencies (Webpack, TypeScript Loader):**

    ```
    npm install --save-dev webpack webpack-cli webpack-dev-server ts-loader html-webpack-plugin
    ```

5.  **Initialize TypeScript Configuration:**

    ```
    npx tsc --init
    ```

    *   Then, we modified `tsconfig.json` to include settings like:

        ```
        {
          "compilerOptions": {
            "target": "es5",
            "lib": ["dom", "dom.iterable", "esnext"],
            "allowJs": true,
            "skipLibCheck": true,
            "esModuleInterop": true,
            "allowSyntheticDefaultImports": true,
            "strict": true,
            "forceConsistentCasingInFileNames": true,
            "noFallthroughCasesInSwitch": true,
            "module": "esnext",
            "moduleResolution": "node",
            "resolveJsonModule": true,
            "isolatedModules": true,
            "noEmit": false,
            "jsx": "react-jsx"
          },
          "include": ["src"]
        }
        ```

6.  **Create Source Directory and Initial File:**

    ```
    mkdir src
    touch src/index.tsx
    ```

    *   We populated `src/index.tsx` with the basic React rendering code, remembering to use the correct import for `ReactDOM` from  `'react-dom/client'`.

7.  **Create Public Directory and HTML File:**

    ```
    mkdir public
    touch public/index.html
    ```

    *   We created a basic `index.html` in the `public` directory with a `div` element with `id="root"`.

8.  **Create `webpack.config.js`:**

    *   We created `webpack.config.js` with the following content (adjusting paths as needed):

        ```
        const path = require('path');
        const HtmlWebpackPlugin = require('html-webpack-plugin');

        module.exports = {
          entry: './src/index.tsx',
          output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js',
          },
          resolve: {
            extensions: ['.ts', '.tsx', '.js'],
          },
          module: {
            rules: [
              {
                test: /\.(ts|tsx)$/,
                use: 'ts-loader',
                exclude: /node_modules/,
              },
            ],
          },
          plugins: [
            new HtmlWebpackPlugin({
              template: './public/index.html',
            }),
          ],
          devServer: {
            static: {
              directory: path.join(__dirname, 'public'),
            },
            compress: true,
            port: 3000,
          },
        };
        ```

9.  **Update `package.json` Scripts:**

    *   We updated the `scripts` section of `package.json` to include the `start` and `build` commands:

        ```
        "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1",
          "start": "webpack serve --mode development",
          "build": "webpack --mode production"
        }
        ```

        ## Project Files and Their Purposes

Our project structure includes several important files, each serving a specific purpose in our React TypeScript application:

1. **package.json**
   - Purpose: Manages project dependencies and scripts.
   - Why: It lists all the libraries our project needs and provides shortcuts for common tasks like starting the development server or building the project.

2. **tsconfig.json**
   - Purpose: Configures TypeScript compiler options.
   - Why: It tells TypeScript how to interpret our code, what features to use, and how strict to be with type checking.

3. **webpack.config.js**
   - Purpose: Configures how our project is built and bundled.
   - Why: It defines how to transform and package our code for the browser, including how to handle different file types and how to optimize the output.

4. **src/index.tsx**
   - Purpose: The entry point of our React application.
   - Why: This is where React starts rendering our app. It's typically where we mount our main component to the DOM.

5. **public/index.html**
   - Purpose: The HTML template for our app.
   - Why: It provides the initial structure that React will populate with our components. It typically includes a root div where our React app is mounted.

6. **.gitignore**
   - Purpose: Specifies which files Git should ignore.
   - Why: Prevents unnecessary files (like node_modules) from being tracked in version control, keeping our repository clean and efficient.

7. **node_modules/ (directory)**
   - Purpose: Contains all installed npm packages.
   - Why: Stores the code for all our project's dependencies, allowing us to use external libraries and tools.

These files work together to create a development environment that compiles TypeScript, bundles our code, and provides a local server for testing our React application. Understanding the role of each file helps in maintaining and extending our project effectively.
