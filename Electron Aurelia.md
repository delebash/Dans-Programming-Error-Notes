If you get error when using Bootstrap in Aurelia

Error: (SystemJS) Bootstrap's JavaScript requires jQuery(…)

AshleyGrant commented on Jun 22
I helped you with this question on Stack Overflow, but I've since investigated a bit more. You can actually remove jQuery as a dependency for your application (so delete it from the dependencies in your package.json). After doing this, I recommend removing the map section of config.js, deleting the jspm_packages folder, and rerunning jspm install.

After doing this, you can actually access bootstrap's jQuery by doing this:

import $ from 'bootstrap';
If doing this doesn't work for you, then your best bet would be to file an issue with JSPM, as the issue you're experiencing is with JSPM and not Aurelia. https://github.com/jspm/jspm-cli


BASE PATH FOR JSPM CONFIG

    "directories": {
      "baseURL": "src"
    },

Full Package Example

      {
      "name": "demoelectronaureliamongodb",
      "title": "Demo Electron ES6, Aurelia MongoDB",
      "version": "1.0.0",
      "description": "Thick client demo app showing Electron, ES6, Aurelia, and MongoDB working together.",
      "main": "main.js",
      "scripts": {
    "start": "electron .",
    "build-mac": "electron-packager . 'DemoElectronAureliaMongoDB' --platform=darwin --arch=x64 --version=0.35.1 --overwrite --out ./build/mac",
    "build-win": "electron-packager . 'DemoElectronAureliaMongoDB' --platform=win32 --arch=ia32 --version=0.35.1 --overwrite --out ./build/win"
      },
      "author": "Karl Shifflett",
      "homepage": "http://karlshifflett.wordpress.com",
      "license": "MIT",
      "keywords": [
    "electron",
    "aurelia",
    "es6",
    "mongodb"
      ],
      "repository": {
    "type": "git",
    "url": "https://github.com/Oceanware/demoelectronaureliamongodb.git"
      },
      "devDependencies": {
    "electron-packager": "^8.1.0",
    "electron-prebuilt": "^1.4.2"
      },
      "jspm": {
    "directories": {
      "baseURL": "src"
    },
    "dependencies": {
      "aurelia-animator-css": "npm:aurelia-animator-css@^1.0.1",
      "aurelia-bootstrapper": "npm:aurelia-bootstrapper@^1.0.0",
      "aurelia-fetch-client": "npm:aurelia-fetch-client@^1.0.0",
      "aurelia-framework": "npm:aurelia-framework@^1.0.4",
      "aurelia-history-browser": "npm:aurelia-history-browser@^1.0.0",
      "aurelia-loader-default": "npm:aurelia-loader-default@^1.0.0",
      "aurelia-logging-console": "npm:aurelia-logging-console@^1.0.0",
      "aurelia-pal-browser": "npm:aurelia-pal-browser@^1.0.0",
      "aurelia-polyfills": "npm:aurelia-polyfills@^1.1.1",
      "aurelia-templating-binding": "npm:aurelia-templating-binding@^1.0.0",
      "aurelia-templating-resources": "npm:aurelia-templating-resources@^1.0.0",
      "aurelia-templating-router": "npm:aurelia-templating-router@^1.0.0",
      "fetch": "github:github/fetch@^1.0.0",
      "font-awesome": "npm:font-awesome@^4.6.3",
      "jquery": "npm:jquery@^3.1.1",
      "text": "github:systemjs/plugin-text@^0.0.9"
    },
    "devDependencies": {
      "babel": "npm:babel-core@^5.8.24",
      "babel-runtime": "npm:babel-runtime@^5.8.24",
      "core-js": "npm:core-js@^1.1.4"
    }
      },
      "dependencies": {
    "pouchdb": "^6.0.6"
      }
    }
    

# ERRORS: #

If you get cannot find app when running electron . but it runs fine if your npm start script which just runs electron .   Check index.js and make sure that loadUrl is changed to loadURL

Also make sure you are in the right directory example if you try to run it in the src folder instead of main you will get this error.