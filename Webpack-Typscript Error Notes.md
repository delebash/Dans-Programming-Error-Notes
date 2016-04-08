# Errors  when importing #

**Cannot resolve file -- jquery is red**

When jquery is red `import $ from 'jquery'` then it means 
no typescript definition file is installed, once installed  and red goes away and it turns green.                                                                                                                                                                                                                                                                      

**Uncaught ReferenceError: require is not defined**

This error shows up in the browser debugger console when you use the import statement without a module loader such as webpack.

The tsc compiler will run successfully but the browser does not know how to import modules so it will give this error.


**Uncaught TypeError: jquery_1.default is not a function**

Error shows up in browser debugger console
This happens because you are using the ES6 syntax `import $ from 'jquery'` statement without using babel to transpile.  Currently browsers that use ES6 do not have support for the import statement so it is necessary to re-compile to ES5 using babel

1) Fix by changing statement to `import $ = require('jquery') `while keeping  target and module as ES5 and commonJs.  In this case babel is not necessary because Typescript knows how to compile this code to ES5

2)Or use babel to transform the code. 
In either case the code is transpiled to ES5

**Cannot find module**

http://jssoup.blogspot.com/2015/06/how-to-use-external-modulelibrary-in.html.

For libs like foundation where the d.ts file is wrong and not giving correct info to locate //lib or module // Although there were errors, the greeter.js file is still created. // You can use TypeScript even if there are errors in your code. But in this case, // TypeScript is warning that your code will likely not run as expected.


**Module parse failed: Unexpected token You may need an appropriate loader to handle this file type.**

Error on WebPack compile
This can happen because you haven't actually installed the webpack loader for this file type such as you forgot to install css-loader

Or This can happen if target=ES6 and you are not using babel

Or if you don't add presets es2015 to babel loader

     loader: 'babel-loader',
          query: {
              presets: ['es2015']
          }
      }

**foundation.js:386 Uncaught ReferenceError: jQuery is not defined**

This means a library is expecting.  
Even though bootstrap works by just using import $ from 'jquery'
Foundation expects jQuery as a global variable and you have to expose it by using the methods below

**Module build failed: Error: Cannot resolve 'file' or 'directory' ./greeter**

Check the extension make sure all have a dot as in `'.ts' not 'ts'`

Example is wrong should be .ts
   	
	resolve: {
        extensions: ['', '.js','ts']
    },

**Module '"jquery"' has no default export**

This is typescript complaining but it still builds ok and you can disable this warning by adding in tsconfig.json

"allowSyntheticDefaultImports": true

**ERROR in Entry module not found: Error: Cannot resolve 'file' or 'directory'**

Check package.json for errors such as extra comma just make sure phpstorm says there are no errors. package.json may not be underlined in red but look to the right for a red circle indicating errors typos in file.
I had **"file-loader, ,"**


#Importing files and modules syntax#

**Modules**
`import jquery = require('jqeury')` translated to new way is `import $ from 'jquery'`

**Static Resources**

`reuire('../styles/styles/css')` translated to new ways is `import '../styles/styles.css'` 

Example:

    import "../node_modules/bootstrap/dist/css/bootstrap.css";
    import '../styles/styles.css'



# Managing Jquery in a project #
You could just import it at every page //import $ from 'jquery' but below is better for jquery libs

Needed for libraries like bootstrap of foundation
See [stackoverflow](http://stackoverflow.com/questions/28969861/managing-jquery-plugin-dependency-in-webpack)

**Use the ProvidePlugin to inject implicit globals**

Just add to webpack.config.js `const ProvidePlugin = require('webpack/lib/ProvidePlugin');` -- **No need to install plugin** via NPM as it comes with webpack

> The ProvidePlugin seems to work in all cases exposing $ and jQuery working with foundation and bootstrap.

Most legacy modules rely on the presence of specific globals, like jQuery plugins do on $ or jQuery. In this scenario you can configure webpack, to prepend jquery everytime it encounters the global $ identifier.

Just add to webpack.config.js `const ProvidePlugin = require('webpack/lib/ProvidePlugin');` -- **No need to install plugin** via NPM as it comes with webpack  

Install 


    plugins: [
        new webpack.ProvidePlugin({
            $: "jquery",
            jQuery: "jquery",
			'window.jQuery': 'jquery'
        })
    ]

OR

**Use expose-loader**

See http://stackoverflow.com/questions/29080148/expose-jquery-to-real-window-object-with-webpack

    npm install expose-loader --save-dev
You can either do this when you require it:


  `import 'expose?$!expose?jQuery!jquery'` -- Only work for $ but not for foundation expecting jQuery not sure why.

or you can do this in your config  -- Does work for now

	loaders: [
    { test: /jquery\.js$/, loader: 'expose?$' },
    { test: /jquery\.js$/, loader: 'expose?jQuery' }
	]

> The ProvidePlugin replaces a symbol in another source through the respective import, but does not expose the symbol on the global namespace. A classic example are jQuery plugins. Most of them just expect jQuery to be defined globally. With the ProvidePlugin you would make sure that jQuery is a dependency (e.g. loaded before) and the occurence of jQuery in their code would be replaced with the webpack raw equivalent of require('jquery').
> 
> If you have external scripts relying on the symbol to be in the global namespace (like let's say an externally hosted JS, Javascript calls in Selenium or simply accessing the symbol in the browser's console) you want to use the expose-loader instead.
> 
> In short: ProvidePlugin manage build-time dependencies to global symbols whereas the expose-loader manages runtime dependencies to global symbols.

Possibly just import the js file import 'path_to_jquery/jquery.min.js'
Then expose global in you page by
    
    window.jQuery = require("jquery");
    window.$ = require("jquery");

Also just for another way to load scripts check out the [imports-loader](https://webpack.github.io/docs/shimming-modules.html)


# Importing Bootstrap #
For any legacy js that relies on jQuery see **Managing Jquery in a project above** 

You will need to add loaders to handle woff2 fonts and png, ect
  
		{ test: /\.html$/, loader: 'html' },
        { test: /\.(png|gif|jpg)$/, loader: 'url', query: { limit: 8192 } },
        { test: /\.woff2(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: 'url', query: { limit: 10000, mimetype: 'application/font-woff2' } },
        { test: /\.woff(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: 'url', query: { limit: 10000, mimetype: 'application/font-woff' } },
        { test: /\.(ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: 'file' },

And install the loaders for each

    npm install html-loader url-loader file-loader --save-dev



# Importing Foundation #
You need to expose jquery as a global either via PluginProvide --prefered method unless noted above or expose-loader.

**Method #1** --Working fine

For foundation 6.2 use the standard import statement

    //No Need to import jquery as it is exposed in webpack.config.js
    import "../node_modules/foundation-sites/dist/foundation.css";
    import "../styles/foundation.css"
    import foundation from 'foundation-sites'

$(document).ready(function () {
    $(document).foundation()
    console.log('foundation lloaded')
});

Webpack.config expose jquery as global

    plugins: [
    new webpack.ProvidePlugin({
    $: "jquery",
    jQuery: "jquery",
    'window.jQuery': 'jquery'
    })
    ],

**Method #2** 

Install script-loader

    npm install script-loader --save-dev
    import 'script!jquery'
    import 'script!what-input'
    import 'script!foundation-sites'

Foundation is working fine but just in case below are some of the articles I used to research this problem

See [foundation issues](https://github.com/zurb/foundation-sites/issues/7386) or [foundation stackoverflow](http://stackoverflow.com/questions/34297788/npm-zurb-foundation-webpack-cannot-resolve-module-foundation/34611081#34611081) for discussions.

# FOUC #

**Webpack**

To help with FOUC for webpack use the extract-text-plugin to extract css into one file that you include in you index.html as normal

Add to webpack.config.js

	const ExtractTextPlugin = require('extract-text-webpack-plugin');

    new ExtractTextPlugin('styles.css', {
            allChunks: true
        })

    // Extract CSS during build
        {
            test: /\.css$/,
            loader: ExtractTextPlugin.extract('style-loader', 'css-loader')
        },

NOTE: the style-loader and css-loader syntax has to be used instead of style!css

**Foundation**

Add these styles to style.css

    .no-js .top-bar {
    display: none;
    }
    
    @media screen and (min-width: 40em) {
    .no-js .top-bar {
    display: block;
    }
    
    .no-js .title-bar {
    display: none;
    }
    }

make sure html tag in index.html file includes this css class
    
    <html class="no-js" lang="en">


# TypeScript #

Using Awsome-Typescript this works by setting useBabel true you do not
need to add a test for babel in webpack.config.js

Also you can either specify preset 2015 here or in babel.rc in you root

    {
      "version": "1.8.9",
      "compileOnSave": false,
      "compilerOptions": {
    "rootDir": "usingES6/",
    "sourceMap": true,
    "target": "es2015",
    "declaration": false,
    "noImplicitAny": false,
    "noResolve": true,
    "removeComments": true,
    "moduleResolution": "node",
    "noLib": false,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true
      },
      "filesGlob": [
    //"./src/**/*.ts",
    "./usingES6/**/*.ts",
    "./test/**/*.ts",
    "./typings/browser.d.ts",
    "./custom_typings/**/*.d.ts",
    "./node_modules/aurelia-*/**/*.d.ts"
      ],
      "exclude": [
    "node_modules",
    "typings/main",
    "typings/main.d.ts"
      ],
      "atom": {
    "rewriteTsconfig": false
      },
      "awesomeTypescriptLoaderOptions": {
     "useBabel": true // use when target ES6
      }
    }


.babelrc

    {
    "presets": ["es2015"]
    }


# wepackconfig.js #

**dirname**

This is a node default that means whatever file you are operating on get its directory so in this case it is the directory of the .webconfig.js
then dirname = "./".  Another example if you had dirname,js then it would find the directory of the js files so if js files are in js/src then dirname would = "js/src"

**path**

This allows you to join a directory with a name to create a new directory
in this case is is "./build"

**output**

The output of the path + file

**resolve extensions**

not sure but you need `['' ,'.js','.ts']`

    var path = require('path');
    const ProvidePlugin = require('webpack/lib/ProvidePlugin');
    const webpack = require("webpack");
    const ExtractTextPlugin = require('extract-text-webpack-plugin');


	module.exports = {
    entry: './src/app.ts',
    output: {
        path: path.join(__dirname, 'build'),
        filename: 'bundle.js'
    },
    resolve: {
        extensions: ['', '.js', '.ts']
    },

    // Adding jquery here makes it global for the app, no import needed
    plugins: [
        // new webpack.ProvidePlugin({
        //     $: "jquery",
        //     jQuery: "jquery",
        //     'window.jQuery': 'jquery'
        // }),
        // new ExtractTextPlugin('styles.css', {
        //     allChunks: true
        // })
    ],
    devtool: 'source-map',
    devServer: {
        host: 'localhost',
        port: 3000
    },
    module: {
        resolve: {
            modulesDirectories: ['node_modules']
        },

**Loaders**

Need one for each file type and you have to install each one such as `npm install html-loader --save-dev`

You can use an array of loaders say for css such as `["style-loader", "css-loader", "sass-loader"]` or pipe them such as `"style!css!sass"` they mean the same.

**Sass**

see example loader for using sass there is a specific order, sass needs to run to create css and then css and use **postcss** to add **autoprefixer**.

Various ways to specify add an additional directory but here is one

	sassLoader: {
      includePaths: [path.resolve(__dirname, "./sass")]
    }

 break-line

       loaders: [
             { test: /\.scss$/, loader: 'style!css?sourceMap!postcss!sass?sourceMap'}
        ]
    },
 	postcss: [
    autoprefixer({
      browsers: ['last 2 versions']
    })
	]
	};
	};

**css**

if you use **ExtractTextPlugin** then a real css file is output in the build directory styles.css and you include this in your index.html per normal


**sourcemaps**
enable in webpack.config.js as seen in example config by setting

    "devtool": "source-map"

enable in tsconfig as well

    "sourceMap": true



**misc**

This test all files in root except node_moduels
for Babel if not using awesome typescript if using ts-loader then you need to add babel test

    { test: /\.js$/, loader: 'babel', exclude: /node_modules/,   query: {presets: ['es2015']}}


**full webpack.config.js**

	var path = require('path');
	const ProvidePlugin = require('webpack/lib/ProvidePlugin');
	const webpack = require("webpack");
	const ExtractTextPlugin = require('extract-text-webpack-plugin');
	const autoprefixer = require('autoprefixer');
	
	module.exports = {
    entry: './src/app.ts',
    output: {
        path: path.join(__dirname, 'build'),
        filename: 'bundle.js'
    },
    resolve: {
        extensions: ['', '.js', '.ts']
    },
    // Adding jquery here makes it global for the app, no import needed
    plugins: [
        new webpack.ProvidePlugin({
            $: "jquery",
            jQuery: "jquery",
            'window.jQuery': 'jquery'
        }),
        new ExtractTextPlugin('styles.css', {
            allChunks: true
        })
    ],
    devtool: 'source-map',
    devServer: {
        host: 'localhost',
        port: 3000
    },
    module: {
        resolve: {
            modulesDirectories: ['node_modules']
        },
        loaders: [
            {test: /\.ts$/, loader: 'awesome-typescript', exclude: [/\.(spec|e2e)\.ts$/, /node_modules/]},
            { test: /\.html$/, loader: 'html' },
            { test: /\.(png|gif|jpg)$/, loader: 'url', query: { limit: 8192 } },
            { test: /\.woff2(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: 'url', query: { limit: 10000, mimetype: 'application/font-woff2' } },
            { test: /\.woff(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: 'url', query: { limit: 10000, mimetype: 'application/font-woff' } },
            { test: /\.(ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: 'file' },
            { test: /\.scss$/, loader: 'style!css?sourceMap!postcss!sass?sourceMap'}
        ]
    },
    postcss: [
        autoprefixer({
            browsers: ['last 2 versions']
        })
    ],
    sassLoader: {
	  includePaths: [path.resolve(__dirname, "./sass")]
	    }
	};




**full ts.config**

	    {
	  "version": "1.8.9",
	  "compileOnSave": false,
	  "compilerOptions": {
    "rootDir": "src/",
    "sourceMap": true,
    "target": "es2015",
    "declaration": false,
    "noImplicitAny": false,
    "noResolve": true,
    "removeComments": true,
    "moduleResolution": "node",
    "noLib": false,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "allowSyntheticDefaultImports": true
	  },
	  "filesGlob": [
	    "./src/**/*.ts",
	    "./typings/browser.d.ts"
	  ],
	  "awesomeTypescriptLoaderOptions": {
	     "useBabel": true // use when target ES6
	  }
	}


# Typings #

This install typescript definition files use --ambient for libraries not in typings npm registry like jquery

    typings install jquery --ambient --save

--save flag save info to typings.json so you can just run 
    typings install

# Package.json #

Normal npm stuff but to use **webpack-dev-server** see the script tags at the top

**full package.json**

		{
	  "name": "starterapp",
	  "version": "1.0.0",
	  "description": "",
	  "main": "webpack.config.js",
	  "scripts": {
    "dev": "webpack-dev-server --config webpack.config.js --inline --progress",
    "build": "webpack --config webpack.config.js --progress --profile",
    "prod": "webpack --config webpack.prod.config.js --progress --devtool source-map",
    "test": "karma start",
    "webdriver:update": "./node_modules/.bin/webdriver-manager update",
    "webdriver:start": "./node_modules/.bin/webdriver-manager start",
    "pree2e": "npm run webdriver:update -- --standalone",
    "e2e": "./node_modules/.bin/protractor"
	  },
	  "author": "",
	  "license": "ISC",
	  "devDependencies": {
    "babel-core": "^6.7.4",
    "babel-loader": "^6.2.4",
    "babel-preset-es2015": "^6.6.0",
    "css-loader": "^0.23.1",
    "extract-text-webpack-plugin": "^1.0.1",
    "file-loader": "^0.8.5",
    "html-loader": "^0.4.3",
    "jquery": "^2.2.2",
    "node-sass": "^3.4.2",
    "sass-loader": "^3.2.0",
    "style-loader": "^0.13.1",
    "url-loader": "^0.5.7",
    "webpack": "^1.12.14",
    "webpack-dev-server": "^1.14.1"
	  }
	}


# Aurelia #

The index.html needs to point to bundle.js not build/bundle.js and needs
to be run through server via `npm run dev`.  Need to research why.

Output to ES5 works but not ES6 unless you use that guys aureliaplugin2 and weback 2.0 and webpack-dev-server 2.0

Targeting ES6 also cause d.ts errors but again the 2.0 version and new aureliaplugin2 fix this I think it does in the other template. TemplateAureliaTSWebpack this uses 2.0 and new plugin.

Targeting ES6 and module commonJs works with many d.ts errors but aurelia loads successfully.  Best to stick with ES5 until wepback 2.0 and new plugin officially supported.  Unless I can use it to import foundation.  Still do not know how bootstrap works as I do not see any bootstrap import in the main.js