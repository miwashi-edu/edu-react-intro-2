# edu-react-intro-2

## Create Project

```bash
#Create directory for react application
mkdir react-app && cd react-app

# Initialize a new Node.js project
npm init -y

# Install React, ReactDOM, and React Scripts
npm install react react-dom 
npm install -D react-scripts

# Set up scripts in package.json
npm pkg set scripts.start="react-scripts start"
npm pkg set scripts.build="react-scripts build"
npm pkg set scripts.test="react-scripts test"
npm pkg set scripts.eject="react-scripts eject"

mkdir {src,public}
```

## Skapa App.js

> Copy paste this as whole and run all at once.

```bash
# Optionally: Create a basic App component
cat > src/App.js << 'EOF'
import React from 'react';
import ReactDOM from 'react-dom';

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
# Optionally: Create a basic index.js file
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
# Optionally: Create a basic index.html file
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



