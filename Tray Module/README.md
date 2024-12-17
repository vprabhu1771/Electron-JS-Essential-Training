The Tray module in Electron allows you to create a system tray icon with a context menu and various functionalities. Below is an example of how to use the Tray module in an Electron application.

---

### Steps to Use the Tray Module

#### 1. **Install an Icon**
Make sure you have an icon file for the tray. For this example, we'll use a `tray-icon.png` file.

---

#### 2. **Modify Your `main.js`**
Add the Tray module to your Electron application.

```javascript
const { app, BrowserWindow, Menu, Tray } = require('electron');
const path = require('path');

let mainWindow;
let tray = null;

function createWindow() {
    mainWindow = new BrowserWindow({
        width: 800,
        height: 600,
        webPreferences: {
            nodeIntegration: true,
        },
    });

    mainWindow.loadFile('index.html');
}

app.whenReady().then(() => {
    createWindow();

    // Create a tray icon
    const iconPath = path.join(__dirname, 'tray-icon.png'); // Ensure you have this file in your project
    tray = new Tray(iconPath);

    // Create a context menu for the tray
    const contextMenu = Menu.buildFromTemplate([
        { label: 'Show App', click: () => mainWindow.show() },
        { label: 'Hide App', click: () => mainWindow.hide() },
        { label: 'Quit', click: () => app.quit() },
    ]);

    // Set the context menu
    tray.setContextMenu(contextMenu);

    // Set tooltip text for the tray icon
    tray.setToolTip('Electron Tray Example');

    // Event to handle clicks on the tray icon
    tray.on('click', () => {
        if (mainWindow.isVisible()) {
            mainWindow.hide();
        } else {
            mainWindow.show();
        }
    });

    app.on('activate', () => {
        if (BrowserWindow.getAllWindows().length === 0) createWindow();
    });
});

app.on('window-all-closed', () => {
    if (process.platform !== 'darwin') app.quit();
});
```

---

#### 3. **Place the Tray Icon**
Save a tray icon file as `tray-icon.png` in the same directory as your `main.js`. For best results:
- Use a 16x16 or 32x32 pixel image.
- PNG format with transparency is ideal.

---

#### 4. **Run the Application**
Start your application:
```bash
npm start
```

---

### What Happens
1. The tray icon appears in your system's notification area.
2. Right-clicking the tray icon shows a context menu with the following options:
   - **Show App**: Displays the main window.
   - **Hide App**: Hides the main window.
   - **Quit**: Exits the application.
3. Clicking the tray icon toggles the visibility of the main window.

---

### Example Project Structure
```
electron-tray-example/
│
├── main.js
├── index.html
├── tray-icon.png
├── package.json
└── node_modules/
```

---

### Tray Icon Example Screenshot
You should see a small icon in the system tray with the specified tooltip and context menu.