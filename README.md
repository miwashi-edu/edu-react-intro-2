# edu-react-intro-2

## Create Project

```bash
#
cd ~
cd ws
rm -rf react-app # If it exists from before.
mkdir react-app && cd react-app
npm init -y

npm install react react-dom

npm install --save-dev webpack
npm install --save-dev webpack-cli
npm install --save-dev webpack-dev-server
npm install --save-dev @babel/core @babel/preset-env
npm install --save-dev @babel/preset-react babel-loader
npm install --save-dev html-webpack-plugin

npm pkg set scripts.start="webpack serve --mode development --open"
npm pkg set scripts.build="webpack --mode production"

mkdir {src,public}
touch ./src/App.jsx
touch ./src/App.css
touch ./src/index.js
touch ./public/index.html
```

## Skapa App.js

```bash
# Create a basic App component
cat > src/App.jsx << 'EOF'
import React from 'react';

function App() {
  return (
    <div>
      <h1>Hello, React!</h1>
    </div>
  );
}
export default App;
EOF
```

## Create index.js

> Copy paste this as whole and run all at once.

```bash
# Create a basic index.js file
cat > src/index.js << 'EOF'
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
EOF
```

# Create index.html

> Copy paste this as whole and run all at once.

```bash
# Create a basic index.html file
cat > public/index.html << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
EOF
```

## Configure babel

```bash
cat > .babelrc << 'EOF'
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
EOF
```

## Configure Webpack

```bash
cat > webpack.config.js << 'EOF'
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'), // Output directory
    filename: 'bundle.js' // Output file
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/, // Handle .js and .jsx files
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader', // Use babel-loader for transpiling JavaScript
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'] // Use presets for modern JS and React
          }
        }
      },
      {
        test: /\.css$/, // Handle CSS files
        use: ['style-loader', 'css-loader'] // Use style-loader and css-loader for CSS
      }
    ]
  },

  resolve: {
    extensions: ['.js', '.jsx'] // Automatically resolve these extensions
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html', // HTML file to use as a template
      filename: 'index.html' // Output filename
    })
  ],
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'), // Directory to serve files from
    },
    compress: true, // Enable gzip compression
    port: 9000, // Port to run the server on
    open: true, // Open the browser after server had been started
    hot: true // Enable hot reloading
  }
};
EOF
```


