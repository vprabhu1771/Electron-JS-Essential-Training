To create a "Hello World" application with Electron, follow these steps:

---

### Prerequisites
1. Install [Node.js](https://nodejs.org/) (LTS recommended).
2. Install a code editor like [Visual Studio Code](https://code.visualstudio.com/).

---

### Steps to Create an Electron Hello World App

#### 1. **Set Up the Project**
1. Create a new directory for your project:
   ```bash
   mkdir electron-hello-world
   cd electron-hello-world
   ```

2. Initialize a new Node.js project:
   ```bash
   npm init -y
   ```

3. Install Electron:
   ```bash
   npm install electron --save-dev
   ```

---

#### 2. **Create Main Script**
1. In your project folder, create a new file named `main.js` with the following content:
   ```javascript
   const { app, BrowserWindow } = require('electron');

   let mainWindow;

   app.whenReady().then(() => {
       mainWindow = new BrowserWindow({
           width: 800,
           height: 600,
           webPreferences: {
               nodeIntegration: true,
           },
       });

       mainWindow.loadFile('index.html');

       app.on('window-all-closed', () => {
           if (process.platform !== 'darwin') {
               app.quit();
           }
       });

       app.on('activate', () => {
           if (BrowserWindow.getAllWindows().length === 0) {
               createWindow();
           }
       });
   });
   ```

---

#### 3. **Create HTML File**
1. Create a new file named `index.html` with the following content:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Hello World</title>
   </head>
   <body>
       <h1>Hello, Electron!</h1>
       <p>Welcome to your first Electron app.</p>
   </body>
   </html>
   ```

---

#### 4. **Update `package.json`**
1. Open your `package.json` file and modify the `scripts` section to include a start command:
   ```json
   "scripts": {
       "start": "electron ."
   }
   ```

---

#### 5. **Run the Application**
1. Start the app by running:
   ```bash
   npm start
   ```

---

You should see a window displaying **"Hello, Electron!"**.

---

### Optional: Folder Structure
Here’s the recommended structure for small Electron projects:
```
electron-hello-world/
│
├── main.js
├── index.html
├── package.json
└── node_modules/
```

Enjoy building with Electron! 🚀