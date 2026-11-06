# J.A.T.E. - Just Another Text Editor

A text editor that runs in the browser, highlights JavaScript syntax, saves your work automatically, and can be installed like a desktop app.

J.A.T.E. is a single-page Progressive Web Application (PWA). It is bundled with webpack, uses Babel so modern JavaScript runs in the browser, and uses a Workbox service worker to cache the app's files.

![J.A.T.E. text editor: a blue header with an Install button and the title "Just Another Text Editor" above a dark code editor showing an ASCII-art banner](client/src/images/1.png)

## About This Project

This is the Progressive Web Applications (PWA) Challenge from a coding boot camp. The goal was to build a text editor that runs in the browser, meets the PWA criteria, and stores data in more than one way. I started from an existing client-server app (starter code provided by the boot camp, 2U) and implemented the parts below.

- **IndexedDB storage** (`client/src/js/database.js`): methods that save and retrieve the editor's content using [idb](https://github.com/jakearchibald/idb), a lightweight wrapper around the IndexedDB API
- **Install button** (`client/src/js/install.js`): handlers for the browser's `beforeinstallprompt` and `appinstalled` events
- **Webpack configuration** (`client/webpack.config.js`): Workbox plugins for the service worker and the web app manifest, plus CSS loaders and Babel

## Features

- **JavaScript syntax highlighting** with the Monokai theme, line numbers, line wrapping and 2-space indentation, powered by [CodeMirror 5](https://codemirror.net/5/)
- **Automatic saving** in your browser using two storage methods: text is stored in `localStorage` as you type, and a copy is written to `IndexedDB` when you click out of the editor
- **Installable**: an Install button in the header lets you add the app to your computer so it opens in its own window
- **Web app manifest and service worker** (built with Workbox) that cache the app's files and let the browser treat it as an installable app

## How to Use

1. Open the app. You will see a dark editor containing an ASCII-art "J.A.T.E." banner written as a JavaScript comment.
2. Click in the editor and type or paste your code or notes. JavaScript is colour-coded as you write it.
3. There is no Save button. Your text is saved automatically, so if you close the tab and come back in the same browser, it is still there.
4. To install the app, click **Install!** in the top-left corner of the header and confirm the browser's prompt. After installing in Chrome, J.A.T.E. appears under Chrome Apps and opens in its own window. You can also launch it from your dock, taskbar or desktop.

Notes on installing:

- Installation works in Chromium-based browsers such as Chrome and Edge. If you click **Install!** and nothing happens, your browser is not offering installation for this page.
- The Install button is hidden on screens narrower than 600px.
- Browsers only allow installation on HTTPS sites or on `localhost`.

## Run It Locally

You need [Node.js](https://nodejs.org/) (the LTS version is fine), which includes npm.

```bash
git clone https://github.com/jveyhl/text_editor.git
cd text_editor
npm install
npm start
```

- `npm install` installs the packages for both the server and the client.
- `npm start` builds the client with webpack, then starts the Express server.

When the terminal prints `Now listening on port: 3000`, open <http://localhost:3000> in your browser. Press `Ctrl+C` in the terminal to stop the server.

After changing any file in `client/src`, stop the server and run `npm start` again so the client is rebuilt.

## Project Structure

```
text_editor/
├── client/
│   ├── src/
│   │   ├── js/
│   │   │   ├── index.js      Starts the editor and registers the service worker
│   │   │   ├── editor.js     Sets up CodeMirror and handles saving text
│   │   │   ├── database.js   Reads and writes IndexedDB using the idb package
│   │   │   ├── install.js    Handles the Install button
│   │   │   └── header.js     The ASCII-art banner shown in a new editor
│   │   └── css/style.css
│   ├── src-sw.js             Service worker (Workbox)
│   ├── webpack.config.js     Bundling, Babel, service worker and manifest setup
│   └── dist/                 Built app that the server serves
└── server/
    └── server.js             Express server that serves client/dist
```

## Built With

- JavaScript (ES6+)
- [CodeMirror 5](https://codemirror.net/5/) for the editor
- [idb](https://github.com/jakearchibald/idb) for IndexedDB
- [Workbox](https://developer.chrome.com/docs/workbox/) for the service worker
- [webpack 5](https://webpack.js.org/) and [Babel](https://babeljs.io/) for bundling
- [Express](https://expressjs.com/) and Node.js for the server

## Credits

Built as a coding boot camp challenge. Starter code was provided by the boot camp (2U).

## License

Released under the MIT License. See the [LICENSE](LICENSE) file for details.
