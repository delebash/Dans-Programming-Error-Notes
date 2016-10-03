## How to Debug Webpack loaders in Webstorm ##

[Npm install instructions](https://www.npmjs.com/package/webpack-webstorm-debugger-script)


    npm install webpack-webstorm-debugger-script

### Add run/debug configuration in WebStorm ###

Add new debug configuration(click + button to add new) of type Node.js and Node parameters: ./node_modules/webpack-webstorm-debugger-script

Put you break points in the css-loader index.ts file

Run debug button

## Install @easy-webpack sass ##
    npm install @easy-webpack/config-sass

**Add easy webpack sass to webpack.config.js and comment out css version**
**MAKE SURE:** you do this in development section

     require('@easy-webpack/config-sass')
        ({ filename: 'styles.css', allChunks: !!ELECTRON, sourceMap: false, extractText: true }),

## Compile css-load ts files on change ##

**First make sure typescript 2.0 is install**

    npm install typescript@next

**install typings in the easy-webpack/config-sass directory**

typings install in the node_modules/@easy-webpack/config-sass folder using commander


## Anytime you make changes to your config-sass file you must recompile with tsc ##

## Use manual tsc compiler ##
open second jetbrains terminal or run in cmder

    tsc --p "F:\Development\GitHub\delebash\Webpack-debug\skeleton-esnext-webpack\node_modules\@easy-webpack\config-sass"
    
src and out put files are set in tsconfig.json so all you need to do for running tsc is point to the root folder were tsconfig.json is located by using the  --p parameter

## If you get errors running tsc  ##
make sure typescript 2.0 is installed and typings under the config-sass folder is installed

**
NOTE:**  Green line in webstorm debugger is showing you the values so you don't have to look at debug window