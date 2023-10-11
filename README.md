# edu-react-intro-2

## Create Project

```bash

```

## Skapa ./src/App.js

```bash
# Create a basic App component
cat > src/App.js << 'EOF'
import React, { useState } from 'react';
import './App.css';

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');

  const handleLogin = () => {
    if (email === 'user@example.com' && password === 'password') {
      setIsLoggedIn(true);
    } else {
      setError('Not authorized');
    }
  };

  const handleLogout = () => {
    setIsLoggedIn(false);
    setEmail('');
    setPassword('');
    setError('');
  };

  return (
    <div className="App">
      {isLoggedIn ? (
        <button onClick={handleLogout}>Log Out</button>
      ) : (
        <div className="login-dialog">
          <input
            type="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
            placeholder="Email"
          />
          <input
            type="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
            placeholder="Password"
          />
          <button onClick={handleLogin}>Log In</button>
          {error && <p className="error">{error}</p>}
        </div>
      )}
    </div>
  );
}

export default App;
EOF
```

## Create ./src/App.css

```bash
cat > src/App.css << 'EOF'
.App {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #2c3e50; /* Darker background for contrast */
  color: #ecf0f1; /* Light text for contrast */
}

.login-dialog {
  background-color: #ecf0f1; /* Lighter background for dialog */
  padding: 20px;
  border-radius: 8px;
  text-align: center;
}

input {
  display: block;
  margin: 10px auto;
  padding: 8px;
  width: 200px;
  border: 1px solid #7f8c8d; /* Subtle border for inputs */
  border-radius: 4px; /* Rounded corners for inputs */
}

button {
  padding: 8px 16px;
  cursor: pointer;
  background-color: #27ae60; /* Green background for button */
  color: #ecf0f1; /* Light text for button */
EOF
```


