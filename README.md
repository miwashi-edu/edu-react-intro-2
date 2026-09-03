# edu-react-intro-2

## Create Project

```bash
#
cd ~
cd ws
rm -rf react-app   # Remove if it exists from before
mkdir react-app && cd react-app
npm init -y
npm install react react-dom
npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/preset-react
mkdir src dist
touch src/App.jsx src/index.js dist/index.html
```

## Skapa App.js

```bash
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
cat > dist/index.html << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div>

    <!-- React and ReactDOM from CDN — no bundler needed -->
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>

    <!-- Our compiled output -->
    <script src="bundle.js"></script>
</body>
</html>
EOF
```

## Configure babel

```bash
cat > .babelrc << 'EOF'
{
  "presets": [
    ["@babel/preset-env", { "modules": "umd" }],
    "@babel/preset-react"
  ]
}
EOF
```

## Add npm Scripts

```bash
npm pkg set scripts.build="babel src --out-file dist/bundle.js"
npm pkg set scripts.start="npm run build && npx serve dist"
```

---

## Run It

```bash
npm start
```

Babel compiles `src/` → `dist/bundle.js`, then `npx serve` starts a local static file server pointing at `dist/`. Open the URL it prints.

To rebuild after changes:

```bash
npm run build
```

---

## What You Just Did — Without Any Magic

| What you wrote | What it does |
|---|---|
| `src/App.jsx` | A React component in JSX syntax |
| `src/index.js` | Entry point — mounts the app into the DOM |
| `dist/index.html` | The page the browser loads |
| `.babelrc` | Tells Babel how to compile your code |
| `npm run build` | Runs Babel → outputs `dist/bundle.js` |
| `npx serve dist` | Serves the `dist/` folder as a website |

When you later use Vite or Create React App, it is doing the same steps — just faster, with hot reload and more configuration. Now you know what's inside the box.

---

> **A note on the CDN scripts in `index.html`:** Loading React from `unpkg.com` keeps the setup simple — it means `bundle.js` can reference `React` and `ReactDOM` as globals without a bundler resolving imports. When you graduate to Vite, the bundler handles that instead, so the CDN tags disappear.


