Currently you have to set typescript to es6 to use the es6 import statement, then babel will compile it to es5

For entry in webpack.config you can leave off the .ts

By just running webpack-dev-server it picks up the webpack.config.js runs index.html on port 8080 and runs
 the entry point.

 The bundle created is all in memory so the index.html bundle path can just be bundle.js

 If running webpack then the if directory in webpack.config.js then it will bundle in that directory
 and if you run on another server e.g. phpstorm then the index.html has to point to the bundle directory of if
 no directory then bundle is created in root




//SETTING UP app.ts

 //import greeter from './greeter';



 //NOTE:
 //No reason to not alwasy target ES6 because babel will then transform to ES5

 //NOTES:
 //t.s.d are critical ts won't working without them as they are pointers to say a node_module
 // Install tsd by running tsd install jquery  --save  you need save to put the path in the main tsd.dts
 // that then points to each libs d.ts

 //NOTES:
 // jquery has Default Export so if targeting ES6 then ES6 import works
 //import $ from "jquery";  //Only if trageting ES6 in tsconfig
 //import $ = require('jquery');  //works target=es5
 //import { jQuery as me } from "jquery";  //doesnt work
 //import * as $ from 'jquery'  //works target = es5 or6


 //NOTES:
 //No default export
 //Bootstrap has no defualt export so you have to use *
 //import whole library


 //TESTING:
 //import boostrap from "bootstrap"; //works es6
 //import * as bootstrap from 'bootstrap' //works es5 and es6
 //import bootstrap = require('bootstrap') //es5


 //Foundation not working can't find module
 //import foundation from "foundation-sites"; //works es6
 import foundation = require('foundation-sites') //es5
 //import * as foundation from "foundation-sites";

 ////NOTE:  CAN'T FIND MODULE ERROR EXPLAINED
 //http://jssoup.blogspot.com/2015/06/how-to-use-external-modulelibrary-in.html
 // For libs like foundation where the d.ts file is wrong and not giving correct info to locate
 //lib or module
 // Although there were errors, the greeter.js file is still created.
 // You can use TypeScript even if there are errors in your code. But in this case,
 // TypeScript is warning that your code will likely not run as expected.

 //import uikit = require('uikit'); //works es5
 //import * as uikit from "uikit"; //works es5 es6
 //import uikit from "uikit"; //works es6

 // $(() => {
 //     var name = 'ggg';
 // alert(name)
 // });



 //NOTES:
 //Diference between var and import is that var is getting a module from an imported library
 //So you have to import express and then get just the http module from the express import
 //import express = require("express")
 //var http = require("http");

 //NOTE:  TSD use Typing instead npm install typings --g
 //https://github.com/typings/typings




 import greeter from './greeter';



 //NOTE:
 //No reason to not alwasy target ES6 because babel will then transform to ES5

 //NOTES:
 //t.s.d are critical ts won't working without them as they are pointers to say a node_module
 // Install tsd by running tsd install jquery  --save  you need save to put the path in the main tsd.dts
 // that then points to each libs d.ts

 //NOTES:
 // jquery has Default Export so if targeting ES6 then ES6 import works
 import $ from "jquery";  //Only if trageting ES6 in tsconfig
 //import $ = require('jquery');  //works target=es5
 //import { jQuery as me } from "jquery";  //doesnt work
 //import * as $ from 'jquery'  //works target = es5 or6


 //NOTES:
 //No default export
 //Bootstrap has no defualt export so you have to use *
 //import whole library


 //TESTING:
 //import boostrap from "bootstrap"; //works es6
 //import * as bootstrap from 'bootstrap' //works es5 and es6
 //import bootstrap = require('bootstrap') //es5


 //Foundation not working can't find module
 //import uikit from "uikit"; //works es6
 //import foundation = require('foundation-sites') //es5
 //import * as foundation from "foundation-sites";

 ////NOTE:  CAN'T FIND MODULE ERROR EXPLAINED
 //http://jssoup.blogspot.com/2015/06/how-to-use-external-modulelibrary-in.html
 // For libs like foundation where the d.ts file is wrong and not giving correct info to locate
 //lib or module
 // Although there were errors, the greeter.js file is still created.
 // You can use TypeScript even if there are errors in your code. But in this case,
 // TypeScript is warning that your code will likely not run as expected.

 //import uikit = require('uikit'); //works es5
 //import * as uikit from "uikit"; //works es5 es6
 //import uikit from "uikit"; //works es6

 $(() => {
     var name = 'sdfasf';
     $(document.body).html(greeter(name));
 });




 //NOTES:
 //Diference between var and import is that var is getting a module from an imported library
 //So you have to import express and then get just the http module from the express import
 //import express = require("express")
 //var http = require("http");

 //NOTE:  TSD use Typing instead npm install typings --g
 //https://github.com/typings/typings



Read this first if you need a refresher  http://www.jbrantly.com/es6-modules-with-typescript-and-webpack/

Currently you have to set typescript to es6 to use the es6 import statement, then babel will compile it to es5

For entry in webpack.config you can leave off the .ts

By just running webpack-dev-server it picks up the webpack.config.js runs index.html on port 8080 and runs
 the entry point.

 The bundle created is all in memory so the index.html bundle path can just be bundle.js

 If running webpack then the if directory in webpack.config.js then it will bundle in that directory
 and if you run on another server e.g. phpstorm then the index.html has to point to the bundle directory of if
 no directory then bundle is created in root


 //NOTE:
 //No reason to not alwasy target ES6 because babel will then transform to ES5

 //NOTES:
 //t.s.d are critical ts won't working without them as they are pointers to say a node_module
 // Install tsd by running tsd install jquery  --save  you need save to put the path in the main tsd.dts
 // that then points to each libs d.ts

 //NOTES:
 // jquery has Default Export so if targeting ES6 then ES6 import works
 //import $ from "jquery";  //Only if trageting ES6 in tsconfig
 //import $ = require('jquery');  //works target=es5
 //import { jQuery as me } from "jquery";  //doesnt work but should for ES5
 //or possibly import { foundation } from 'foundation-sites/js/foundation.core';
 //
 //import * as $ from 'jquery'  //works target = es5 or6


 //NOTES:
 //No default export
 //Bootstrap has no defualt export so you have to use *
 //import whole library


 NOTES: TypeScript Es6 and Import verse Require
 see http://www.jbrantly.com/es6-modules-with-typescript-and-webpack/
 CommonJs uses require
 ES6 uses import

 Also note that the webpack program itself in the webpack.config.js still uses CommonJs.  In 2.0
 webpack.config will support ES6 syntax so you can use import instead of requrie

 //Foundation not working can't find module
 //import foundation from "foundation-sites"; //works es6
 import foundation = require('foundation-sites') //es5
 //import * as foundation from "foundation-sites";

 ////NOTE:  CAN'T FIND MODULE ERROR EXPLAINED
 //http://jssoup.blogspot.com/2015/06/how-to-use-external-modulelibrary-in.html
 // For libs like foundation where the d.ts file is wrong and not giving correct info to locate
 //lib or module
 // Although there were errors, the greeter.js file is still created.
 // You can use TypeScript even if there are errors in your code. But in this case,
 // TypeScript is warning that your code will likely not run as expected.

 //import uikit = require('uikit'); //works es5
 //import * as uikit from "uikit"; //works es5 es6
 //import uikit from "uikit"; //works es6

 // $(() => {
 //     var name = 'ggg';
 // alert(name)
 // });



 //NOTES:
 //Difference between var and import is that var is getting a module from an imported library
 //So you have to import express and then get just the http module from the express import
 //import express = require("express")
 //var http = require("http");

 //NOTE:  TSD use Typing instead npm install typings --g
 //https://github.com/typings/typings




 import greeter from './greeter';



 //NOTE:
 //No reason to not alwasy target ES6 because babel will then transform to ES5

 //NOTES:
 //t.s.d are critical ts won't working without them as they are pointers to say a node_module
 // Install tsd by running tsd install jquery  --save  you need save to put the path in the main tsd.dts
 // that then points to each libs d.ts

 //NOTES:
 // jquery has Default Export so if targeting ES6 then ES6 import works
 import $ from "jquery";  //Only if trageting ES6 in tsconfig
 //import $ = require('jquery');  //works target=es5
 //import { jQuery as me } from "jquery";  //doesnt work
 //import * as $ from 'jquery'  //works target = es5 or6


 //NOTES:
 //No default export
 //Bootstrap has no defualt export so you have to use *
 //import whole library


 //TESTING:
 //import boostrap from "bootstrap"; //works es6
 //import * as bootstrap from 'bootstrap' //works es5 and es6
 //import bootstrap = require('bootstrap') //es5


 //Foundation not working can't find module
 //import uikit from "uikit"; //works es6
 //import foundation = require('foundation-sites') //es5
 //import * as foundation from "foundation-sites";

 ////NOTE:  CAN'T FIND MODULE ERROR EXPLAINED
 //http://jssoup.blogspot.com/2015/06/how-to-use-external-modulelibrary-in.html
 // For libs like foundation where the d.ts file is wrong and not giving correct info to locate
 //lib or module
 // Although there were errors, the greeter.js file is still created.
 // You can use TypeScript even if there are errors in your code. But in this case,
 // TypeScript is warning that your code will likely not run as expected.

 //import uikit = require('uikit'); //works es5
 //import * as uikit from "uikit"; //works es5 es6
 //import uikit from "uikit"; //works es6

 $(() => {
     var name = 'sdfasf';
     $(document.body).html(greeter(name));
 });




 //NOTES:
 //Diference between var and import is that var is getting a module from an imported library
 //So you have to import express and then get just the http module from the express import
 //import express = require("express")
 //var http = require("http");

 //NOTE:  TSD use Typing instead npm install typings --g
 //https://github.com/typings/typings

NOTES: Import css:
NOTES: Import css:
npm install style-loader css-loader --save-dev
add { test: /\.css$/, loader: "style-loader!css-loader" },
Import in module such as app.ts
import "./styles.css";

NOTES: REQUIRE
In app.ts import is used, but the reason you see require in the webackconfig is because webpack itself uses
commonJs for its program and config is processed by webpack

Importing CSS
import 'styles.css'  if targeting ES5 works fine
If targeting ES6 and ES6 modules then fails unless using webpack 2.0 which supports import statements
You can fix this by targeting ES6 but using commonJs as module format

Typings
orig
declare module "Foundation" {
    export = Foundation;
}
es6
 export default MyLib;



