# Async/Await #

    npm install babel-preset-env  --save-dev


**For evergreen browsers that already support generators:**

To use asnyc await you need to have es6 generators working -- for evergreen browsers generators are working

You cannot use presets because it tries to convert generators which then require the regeneratorRuntime. Instead we have to add the plugins from the es2015,2016,2017 presets manually as in the below .babelrc config

**NOTE:**
All current browsers support generators and
Chrome,FF,Safari also support async functions so we can just 
remove the async transform and use native async functions

	"transform-async-to-generator",
    "transform-async-generator-functions"

and replace with  -- the below just allows babel to parse but not transform

	"syntax-async-functions"

For now we are leaving async-tranforms in place to support older browsers

Add plugins manually

	"plugins": [
    "syntax-flow",
    "transform-decorators-legacy",
    "transform-flow-strip-types",
    
	"transform-async-to-generator",
    "transform-async-generator-functions",
    "transform-object-rest-spread",
    "transform-class-properties",
    "transform-export-extensions",

    "transform-es2015-arrow-functions",
    "transform-es2015-block-scoped-functions",
    "transform-es2015-block-scoping",
    "transform-es2015-classes",
    "transform-es2015-computed-properties",
    "transform-es2015-destructuring",
    "transform-es2015-duplicate-keys",
    "transform-es2015-for-of",
    "transform-es2015-function-name",
    "transform-es2015-literals",
    "transform-es2015-modules-commonjs",
    "transform-es2015-object-super",
    "transform-es2015-parameters",
    "transform-es2015-shorthand-properties",
    "transform-es2015-spread",
    "transform-es2015-sticky-regex",
    "transform-es2015-template-literals",
    "transform-es2015-typeof-symbol",
    "transform-es2015-unicode-regex"
	]

**For Older browsers:** needing a polyfill for generators then we can use presets and **install generator polyfill** per instructions below
    
	"presets": [
    ["env", {
      "targets": {
    "browsers": ["last 2 versions"]
      }
    }],
    "stage-1"
      ],


**Generator polyfill** for browsers that do not support generators

Install as run-time dependency

    npm install regenerator-runtime  --save

Then

    import regeneratorRuntime from 'regenerator-runtime';
    window.regeneratorRuntime = regeneratorRuntime;

For aurelia-cli you need to add to **aurelia.json**

     {
            "name": "regenerator-runtime",
            "path": "../node_modules/regenerator-runtime",
            "main": "runtime-module"
          },


Examples:

Generator
    
      * genFunc() {
    console.log('First');
    yield; // (A)
    console.log('Second'); // (B)
      }

    let genObj = this.genFunc();
    genObj.next()


Async

    // fake asynchronise operation
    function fakeop(ms) {
      return new Promise(r => setTimeout(r, ms));
    }


    async function foo() {
      await fakeop(500);
      throw Error('bar');
    }
    
    foo()


    async function logFetch(url) {
      try {
    const response = await fetch(url);
    console.log(await response.text());
      }
      catch (err) {
    console.log('fetch failed', err);
      }
    }




welcome.js

      submit() {
     // let genObj = this.genFunc();
     //genObj.next()
      this.hello()
      }
    
      canDeactivate() {
    if (this.fullName !== this.previousValue) {
      return confirm('Are you sure you want to leave?');
    }
      }
    
      // // fake asynchronise operation
      fakeop(ms) {
    return new Promise(r => setTimeout(r, ms));
      }
      wait(ms) {
    return new Promise(r => setTimeout(r, ms));
      }
    
      async  hello() {
    await this.fakeop(1000);
    console.log('test')
      }
    
      * genFunc() {
    console.log('First');
    yield; // (A)
    console.log('Second'); // (B)
      }

See
https://babeljs.io/docs/plugins/syntax-async-functions/

