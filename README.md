# edu-react-intro-2

## Create Project

```bash
#
cd ~
cd ws
rm -rf react-app # If it exists from before.

#Create directory for react application
mkdir react-app && cd react-app

# Initialize a new Node.js project
npm init -y

# Install React, ReactDOM, and React Scripts
npm install react react-dom
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
#npm install -D react-scripts

# Set up scripts in package.json
npm pkg set scripts.start="webpack serve --mode development --open"
npm pkg set scripts.build="webpack --mode production"
#npm pkg set scripts.start="react-scripts start"
#npm pkg set scripts.build="react-scripts build"
#npm pkg set scripts.test="react-scripts test"
#npm pkg set scripts.eject="react-scripts eject"

mkdir {src,public}
touch ./src/App.jsx
touch ./src/App.css
touch ./src/index.js
touch ./public/index.html
```

## Skapa App.js

> Copy paste this as whole and run all at once.

```bash
# Create a basic App component
cat > src/App.jsx << 'EOF'
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

```
cat > webpack.config.js << 'EOF'
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
        test: /\.jsx?$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      }
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
  ],
  devServer: {
    contentBase: path.join(__dirname, 'dist'),
    compress: true,
    port: 9000,
  },
};
EOF
```

## Run the application first time

> You will be asked to add browser support to your package.json, accept that!

```bash
# Start the application
npm start

? We're unable to detect target browsers.

Would you like to add the defaults to your package.json? › (Y/n)y
```

### Added to your package.json

> Just answer yes, and this will be added.
> This tells the transpiler what requirement your application will support.

```json
"browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
```
## Add the missing dependency

> Add  --loglevel=error or --silent when adding development dependencies, otherwise react-scripts will warn.

```
npm install -D @babel/plugin-proposal-private-property-in-object  --loglevel=error
```



