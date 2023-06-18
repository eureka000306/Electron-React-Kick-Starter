npm create-react-app electron-react-demo
cd electron-react-demo
npm uninstall web-vitals
del src\reportWebVitals.js
npm install @craco/craco
create craco.config.js in root directory

fill the file with the code lines
const nodeExternals = require("webpack-node-externals");
module.exports = {
  webpack: {
    configure: {
      target: "electron-renderer",
      externals: [
        nodeExternals({
          allowlist: [/webpack(\/.*)?/, "electron-devtools-installer"],
        }),
      ],
    },
  },
};

npm install webpack-node-externals --save-dev
npm install electron --save-dev
type nul > public\electron.js

fill electron.js file with this code lines
const electron = require("electron");
const path = require("path");
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;
let mainWindow;
function createWindow() {
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: { nodeIntegration: true, contextIsolation: false },
  });
  mainWindow.loadFile(path.join(__dirname, "../build/index.html"));
}
app.on("ready", createWindow);

add this code line to package.json file
  "main": "public/electron.js",
  "homepage": "./",

"script": {
"build": "craco build",
"start": "electron ."
}

npm run build
npm start
npm install electron-packager --save-dev
npm install electron-packager -g
cd ..

electron-packager electron-react-demo electron-tough-starter --platform=win32 --arch=x64
--arch=darwin for marOC
--arch-linux for Linux