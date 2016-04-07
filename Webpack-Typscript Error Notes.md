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
