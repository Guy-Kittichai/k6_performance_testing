# 📋 k6 & VS Code Setup Guide

This guide covers the installation of the **k6 Engine** and the complete setup of **Visual Studio Code (VS Code)** for the load testing course.

---

## 1. Install k6 Engine
Choose the installation method based on your operating system (OS):

### 🪟 Windows
* **Method 1:** Download and install via the official [k6 Installer (MSI)](https://k6.io "k6 Windows Installer").
* **Method 2:** Open PowerShell and run:
  ```bash
  winget install grafana.k6
  ```

### 🍏 macOS
* Open Terminal and install via Homebrew:
  ```bash
  brew install k6
  ```

### 🐧 Linux (Ubuntu/Debian)
* Open Terminal and run:
  ```bash
  sudo gpg --no-default-keyring --keyring /usr/share/keyrings/grafana.gpg --keyserver hkps://keys.openpgp.org --recv-keys 963FA27E7D9A3B54A7B5DE103E14E6E601B79E23
  echo "deb [signed-by=/usr/share/keyrings/grafana.gpg] https://grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
  sudo apt-get update
  sudo apt-get install k6
  ```

---

## 2. Install Visual Studio Code
* 📥 **Download Code Editor:** Get the installer directly from the [Official Visual Studio Code Website](https://visualstudio.com "Download VS Code").

---

## 3. Required VS Code Extensions
Open VS Code, navigate to the Extensions marketplace (`Ctrl+Shift+X` or `Cmd+Shift+X`), and install these plugins:

* **k6 (Grafana):** Provides syntax highlighting, code snippets, and k6 commands execution.
* **Prettier - Code formatter:** Automatically cleans up and formats your script for readability.
* **ESLint:** Checks for JavaScript errors and syntax issues in real time.

---

## 4. Enable Code Autocompletion (IntelliSense)
To get smart autocomplete (e.g., suggesting `http.get` or `check` as you type), follow these steps:

1. Ensure **Node.js** is installed on your computer ([Download Node.js](https://nodejs.org "Nodejs Official Download")).
2. Open your project folder in VS Code.
3. Open the built-in terminal (`Ctrl+``) and run:
   ```bash
   npm install --save-dev @types/k6
   ```
4. VS Code will now automatically suggest k6 modules, methods, and parameters!

---

## 5. First Test Script (Verification)
Let's create a quick script to verify that your k6 installation and VS Code autocomplete are working perfectly.

1. In VS Code, create a new file named `script.js`.
2. Copy and paste the following code into `script.js`:

```javascript
import http from 'k6/http';
import { sleep, check } from 'k6';

export const options = {
  vus: 1,           // 1 Virtual User
  duration: '5s',   // Run for 5 seconds
};

export default function () {
  // Send a GET request to the k6 test site
  const res = http.get('https://k6.io');

  // Check if the response status is 200
  check(res, {
    'status is 200': (r) => r.status === 200,
  });

  sleep(1);
}
```

3. Open your terminal in VS Code (`Ctrl+``) and run the script using the command below:
```bash
k6 run script.js
```
*If successful, you will see the test execution summary in your terminal with a green checkmark next to `"status is 200"`.*
