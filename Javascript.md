# Async/Await #

 
**For evergreen browsers that already support generators:**

However since we are still using babel we are still using a preset for converting to ES6. The default preset includes `"transform-async-to-generator","transform-async-generator-functions"`  **This will cause an error saying regenerator-runtime is missing** So we just need to install plugins manually instead of using preset.


Evergreen install instructions:

   `npm install babel-preset-env  --save-dev`

Note: we are not actually using the above preset, it is just an easy way to install all plugins we need

`"syntax-async-functions"` is used for something can't remember now so just leave out 

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

**For Older browsers Install regenerator-runtime polyfill:** 

Install as run-time dependency

    npm install regenerator-runtime  --save

Then in main.js

    import regeneratorRuntime from 'regenerator-runtime';
    window.regeneratorRuntime = regeneratorRuntime;

For aurelia-cli you also need to add it to **aurelia.json**

     {
            "name": "regenerator-runtime",
            "path": "../node_modules/regenerator-runtime",
            "main": "runtime-module"
          },


**Examples:**

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

