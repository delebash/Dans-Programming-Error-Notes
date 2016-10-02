# You Have to re-compile LevelDown (part of LevelDB) for Electron #

The below command works to recompile leveldown

    ./node_modules/.bin/electron-rebuild -w leveldown -p

Also for help

    ./node_modules/.bin/electron-rebuild -h

# Manual Build in case electron-rebuild fails which is for me now #

Steps to re-build leveldown or any module for electron:
 
    cd node_modules/leveldown
    node-gyp rebuild --target=1.4.2 --arch=x64 --dist-url=https://atom.io/download/atom-shell

The target is the version of electron you are using
You need to cd into the module you want to build
as in `cd /node_modules/levledown` then run the above command adjusted for the version of electron installed

References

[https://github.com/nodejs/node-gyp](https://github.com/nodejs/node-gyp)

[https://github.com/electron/electron/blob/master/docs/tutorial/using-native-node-modules.md](https://github.com/electron/electron/blob/master/docs/tutorial/using-native-node-modules.md)

[https://github.com/nodejs/node-gyp](https://github.com/nodejs/node-gyp)

**End Build Instructions**


**Package.json for Electron Aurelia LevelDownPouch Example**


In the package.json you can specify where you want the jspm_modules to be installed as in below

    "jspm": {
    "directories": {
      "baseURL": "src"
    },
    
But you don' have to you can leave in it the main project like the 
aurelia-skeleton examples
This way all the info is under the src folder but It might be better to leave it the normal way and have the jspm_modules installed under root just like node_modules


**Full package.json example for AureliaPouchLevelDB**

    {
      "name": "aurelia-skeleton-navigation",
      "version": "1.0.0",
      "description": "A starter kit for building a standard navigation-style app with Aurelia.",
      "keywords": [
    "aurelia",
    "navigation",
    "skeleton"
      ],
      "homepage": "http://aurelia.io",
      "bugs": {
    "url": "https://github.com/aurelia/skeleton-navigation/issues"
      },
      "license": "CC0-1.0",
      "author": "Rob Eisenberg <rob@bluespire.com> (http://robeisenberg.com/)",
      "main": "main.js",
      "repository": {
    "type": "git",
    "url": "http://github.com/aurelia/skeleton-navigation"
      },
      "scripts": {
    "start": "electron .",
    "build-mac": "electron-packager . 'DemoElectronAureliaMongoDB' --platform=darwin --arch=x64 --version=0.35.1 --overwrite --out ./build/mac",
    "build-win": "electron-packager . 'DemoElectronAureliaMongoDB' --platform=win32 --arch=ia32 --version=0.35.1 --overwrite --out ./build/win"
      },
      "devDependencies": {
    "aurelia-bundler": "^0.4.0",
    "aurelia-tools": "^0.2.4",
    "babel": "^6.5.2",
    "babel-core": "^6.11.4",
    "babel-eslint": "^6.1.2",
    "babel-plugin-syntax-flow": "^6.8.0",
    "babel-plugin-transform-decorators-legacy": "^1.3.4",
    "babel-plugin-transform-es2015-modules-amd": "^6.8.0",
    "babel-plugin-transform-es2015-modules-commonjs": "^6.11.5",
    "babel-plugin-transform-es2015-modules-systemjs": "^6.12.0",
    "babel-plugin-transform-flow-strip-types": "^6.8.0",
    "babel-preset-es2015": "^6.9.0",
    "babel-preset-es2015-loose": "^7.0.0",
    "babel-preset-stage-1": "^6.5.0",
    "conventional-changelog": "1.1.0",
    "electron": "^1.4.1",
    "electron-packager": "^8.0.0",
    "electron-rebuild": "^1.2.1",
    "isparta": "^4.0.0",
    "istanbul": "^1.0.0-alpha.2",
    "jasmine-core": "^2.4.1",
    "jspm": "^0.16.41",
    "karma": "^1.1.2",
    "karma-babel-preprocessor": "^6.0.1",
    "karma-chrome-launcher": "^1.0.1",
    "karma-coverage": "^1.1.1",
    "karma-jasmine": "^1.0.2",
    "karma-jspm": "2.2.0"
      },
      "jspm": {
    "directories": {
      "baseURL": "src"
    },
    "dependencies": {
      "aurelia-animator-css": "npm:aurelia-animator-css@^1.0.0-rc.1.0.0",
      "aurelia-bootstrapper": "npm:aurelia-bootstrapper@^1.0.0-rc.1.0.0",
      "aurelia-fetch-client": "npm:aurelia-fetch-client@^1.0.0-rc.1.0.0",
      "aurelia-framework": "npm:aurelia-framework@^1.0.0-rc.1.0.0",
      "aurelia-history-browser": "npm:aurelia-history-browser@^1.0.0-rc.1.0.0",
      "aurelia-loader-default": "npm:aurelia-loader-default@^1.0.0-rc.1.0.0",
      "aurelia-logging-console": "npm:aurelia-logging-console@^1.0.0-rc.1.0.0",
      "aurelia-pal-browser": "npm:aurelia-pal-browser@^1.0.0-rc.1.0.0",
      "aurelia-polyfills": "npm:aurelia-polyfills@^1.0.0-rc.1.0.0",
      "aurelia-router": "npm:aurelia-router@^1.0.0-rc.1.0.0",
      "aurelia-templating-binding": "npm:aurelia-templating-binding@^1.0.0-rc.1.0.0",
      "aurelia-templating-resources": "npm:aurelia-templating-resources@^1.0.0-rc.1.0.0",
      "aurelia-templating-router": "npm:aurelia-templating-router@^1.0.0-rc.1.0.0",
      "babel": "npm:babel-core@^5.8.24",
      "bluebird": "npm:bluebird@3.4.1",
      "bootstrap": "github:twbs/bootstrap@^3.3.6",
      "fetch": "github:github/fetch@^1.0.0",
      "font-awesome": "npm:font-awesome@4.6.3",
      "jquery": "npm:jquery@^2.2.4",
      "text": "github:systemjs/plugin-text@^0.0.8"
    },
    "devDependencies": {
      "babel-runtime": "npm:babel-runtime@^5.8.24",
      "core-js": "npm:core-js@^1.1.4"
    }
      }
    }

Other Package with pouchbd

    {
      "name": "demoelectronaureliamongodb",
      "version": "1.0.0",
      "bundle": "com.democode.demoelectronaureliamongodb",
      "description": "Thick client demo app showing Electron, ES6, Aurelia, and MongoDB working together.",
      "repository": {
    "type": "git",
    "url": ""
      },
      "keywords": [
    "aurelia",
    "electron",
    "es6",
    "mongodb"
      ],
      "author": "Karl R. Shifflett",
      "homepage": "http://karlshifflett.wordpress.com",
      "license": "MIT",
      "electron": "^1.4.1",
      "electron-rebuild": "^1.2.1",
      "dependencies": {
    "pouchdb": "^6.0.5"
      }
    }
