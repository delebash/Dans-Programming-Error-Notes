To use ES6 generators you need to 

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

To use asnyc await you need to have es6 generators working according to above instructions then

    npm install babel-preset-env  --save-dev

.babelrc presets

      "presets": [
    ["env", {
      "targets": {
    "browsers": ["last 2 versions"]
      }
    }],
    "stage-1"
      ],


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