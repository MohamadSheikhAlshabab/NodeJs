- Require : use it to depend on any library, whether this library is bulit-in one like HTTP or if it's third-party installed library.
- process.stdin.read() : use it to read from user's input. it's like prompt()
- process.stdout.write() : use it to write user's input. it's like console.log()
- process.exit() : use it to terminate the process.

### Destructuring :

- all these constants :


      const PI = Math.PI;
      const SQRT2 = Math.SQRT2;
      const E = Math.E;
      
equals to :

`const {PI, E, SQRT2} = Math;`

- EX #2:



        const circle = {
          label: 'circleX',
          raduis: 2,
         };
                                        //// this is second parameter with default value and it's optional because of (={})
        const circleArea = ({ raduis }, { precision = 2 } = {}) => (PI * raduis * raduis).toFixed(2);

        console.log(circleArea(circle)); // 12.56

        console.log(circleArea(circle, { percision : 5})); // 12.56637
                  
                  
- ex #3: destructuring with array

      const [ first, second, , forth] = [10, 20, 30, 40];
      first // 10 
      second // 20 
      forth // 40


### Rest Operator: 

    const [ first, ...restOfItem ] = [ 10, 20, 30, 40 ];
    first // 10
    restOfItem // [ 20, 30, 40 ] create new array to hold the rest items of array after pop out the first element.

- ex #2:

      const data = {
        temp1: '001',
        temp2: '002',
        firstName: 'John',
        lastName: 'Doe',
      };

      const { temp1, temp2, ...person } = data;


### Spread Operator:
- spread one array or object into a new array or object, it's useful for copying arrays and objects, but it's shallow copy (any nested objects or arrays will be shared between these copies). 

      const newArray = [ ...restOfItem ];
      const newObject = { ...person };

---

- Everthing in Javascript is an object, including functions.
- A _class_ : is a template or buleprint for you to define shared structure and behavior between similar objects.

---
### NPM :
- what is package?
  - the name package is what npm uses to label the bits of reusable code.

- Node Package : is basically a folder that contains scripts that can be run by node.
- which is to say any folder that has some javascript code in it is basically a node package.
- another name that is commonly used  to  describe a code folder in node is module.

- `npm i -D nodemon` -D means this for develoment not for production. and in package.json under name "devDependencies"

----

### Semantic Versioning (SemVer):

- Major (Breaking Changes). Minor (Backward Compatible). Patch (Bug Fixes)
- tilde (for patch): ~1.2.3 means 1.2.x which is x any number greater or equal to 3. ex: 1.2.10 ok, 1.2.1 ok, 1.3.0 not ok. 
- caret (for minor): ^1.2.3 means 1.x.y which is x any number greater or equal to 2 , and y can be any thing. ex: 1.10.100 ok, 1.1.1 not ok, 1.2.0 ok, 1.10.0 ok, 2.0.0 not ok.

- semver.npmjs.com

---

- `console.log(arguments);`
-  it's outputs exactly 5 arguments, which node passed to hidden wrapping function when it executes your file.
-  so you should remember that every time you hear the word module. this is not just a file. it's a function that receives arguments, and it will also return something.
-  what is exactly happend in previous example:

        // function (exports, module, require, __filename, __diname){ // bulit-in hidden wrapping function
             console.log(arguments);
        // }

- you can use exports or module.exports to define the API of a module.
- you can use require to require other modules inside this one.
- `__filename` has the path to this file.
- `__dirname` has the path to the folder hosting this file.
- all these objects, you can use in this file, are not global objects, they are just arguments to the wrapping function.
- they are customized for each file. and they're different in each file.
- if define a variable in top level, it's not global variable at all. it's just a variable inside a function. the scope of it is the hidden wrapping function.
- if define a variable inside browser in a script(browsers does not have hidden wrapping function), it will be global and available to all scripts you include after defining it.
 - bulit-in wrapping function return be default (return module.exports) this is what returns all the times for every file.
 - exports is just alias to module.exports.
 
 ----
 
 ## Examples of module APIs:
 
 1- Top-level API is a simple object (no need to use module.exports)
 
  - file1.js
  
        exports.language = "English";
        exports.direction = "RTL";
        exports.encoding = "UTF-8";
        
        
    file2.js
   
      
        const api = require('./file1');
        console.log(api.language, api.direction, api.encoding); English RTL UTF-8
      
2- Top-level API is an array:

  - file1.js
  
        module.exports = [2, 3, 5, 7];
       
  - file2.js

        console.log(require('./file1')); // [2, 3, 5, 7]
      
      
 3- Top-level API is a string:
 
 
  - file1.js // this file is returning a template string
  
        module.exports =`   // this is backtick (because  is multiline template string)
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>Document</title>
            </head>
            <body>

            </body>
            </html>
            `
       
       
 - file2.js
  
      
        const myTemplate = require('./file1');
        console.log(myTemplate);
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>Document</title>
            </head>
            <body>
            
            
 4- Top-level API is a function:
 
 
  - file1.js // this file is returning a template string
  
        module.exports = title => ` // this is backtick (because  is multiline template string)
       
       
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>${title}</title>
            </head>
            <body>

            </body>
            </html>
            `
       
       
 - file2.js
  
      
        const templateGenerator = require('./file1');
        const myTemplate = templateGenerator('Hello Node!');
        console.log(myTemplate);
        
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>Hello Node!</title>
            </head>
            <body>

            </body>
            </html>
      

            </body>
            </html>
            
---

## Node's Global Object:

- The only global variables in Node are the variables attached to this (global) special global object.
- this global object is the equivalent to the window object in browsers, and it's the only global concept in Node.
- all of (console.dir(global,{depth:0}))  these are globally available in all node modules 


           console.dir(global,{depth:0}) // use dir trick here to only show the top-level properties on this object
            <ref *1> Object [global] {
              global: [Circular *1],
              clearInterval: [Function: clearInterval],
              clearTimeout: [Function: clearTimeout],
              setInterval: [Function: setInterval],
              setTimeout: [Function],
              queueMicrotask: [Function: queueMicrotask],
              performance: [Performance [EventTarget]],
              clearImmediate: [Function: clearImmediate],
              setImmediate: [Function]
            }
      
      
  - EX:

    - file1.js:
          
          global.answer = 42;
     
    - file2.js:

          require('file1.js');
          console.log(answer); // 42
          
          
          
---

## Event Loop:

- what node uses to process asynchronous actions and interface them for you so that you don't have to deal with threads.

---
## Error VS Exceptions:

- An __ERROR__ is simply a problem, an unknown problem, Applications are not prepared to deal with it.
- An __EXCEPTION__ is a condition that applications know about and are prepared to deal with it, they catch that condition and do something with it.


- EX #1:

        const fs = require('fs');
        const files = ['file1.js', 'file2.js'];
        
        files.forEach(file => {
          const data = fs.readFileSync(file);
          console.log('File data is', data);
        });

        File data is <Buffer 63 6f 73 ... 126 more bytes>
        File data is <Buffer 63 6f 73 ... 207 more bytes>

- EX #2: // Node will crash and exit because we inject file not exist

        const fs = require('fs');
        const files = ['file1.js', 'file2.js', 'zzz.js']; // (zzz.js) file not exist
        
        files.forEach(file => {
          const data = fs.readFileSync(file);
          console.log('File data is', data);
        });

        File data is <Buffer 63 6f 73 ... 126 more bytes>
        File data is <Buffer 63 6f 73 ... 207 more bytes>
        
        throw err;
        ^
        
        Error: ENOENT: no such file or directory, open 'zzz.js'
        
- EX #3: // use try catch to handle the errors


        
        const fs = require('fs');
        const files = ['file1.js', 'file2.js', 'zzz.js']; // (zzz.js) file not exist
        
        files.forEach(file => {
          try{
              const data = fs.readFileSync(file);
              console.log('File data is', data);
          } catch (err) {
              console.log('File not found');
          }
        });
        
        
        
        File data is <Buffer 63 6f 73 ... 126 more bytes>
        File data is <Buffer 63 6f 73 ... 207 more bytes>
        File not found
        
        
        
- EX #4:



        
        const fs = require('fs');
        const files = ['file1.js', 'file2.js', 'zzz.js']; // (zzz.js) file not exist
        
        files.forEach(file => {
          try{
              const data = fs.readFileSync(file,'utf-8');
              console.log('File data is', data);
          } catch (err) {
              console.log('File not found');
          }
        });
        
        
        
        File not found
        File not found
        File not found
        
- EX # 5:

        const fs = require('fs');
        const files = ['file1.js', 'file2.js', 'zzz.js']; // (zzz.js) file not exist
        
        files.forEach(file => {
          try{
              const data = fs.readFileSync(file);
              console.log('File data is', data);
          } catch (err) {
              if (err.code === 'ENOENT'){
                  console.log('File not found');
              } else {
                  throw err;
              }
          }
        });
        
        
        
        File data is <Buffer 63 6f 73 ... 126 more bytes>
        File data is <Buffer 63 6f 73 ... 207 more bytes>
        File not found
        
        
---

## Node's Asynchronous Patterns :

- EX #1: Sync

        const fs = require('fs');
        const data = fs.readFileSync(__filename);
        console.log('File data is',data);
        console.log('TEST');
        
        
        File data is <Buffer 63 67 6f 6e ...>
        TEST
        
- EX #2: callBack Pattern:


- basically, this code was executed in two iterations of event loop.
- the first iteration executed readFile itself and the console log TEST line and that first iteration only defined the callback function.And also, in the same iteration, Node will ask the operating system for data. Later on, once the operating system is ready with data, and this could be a few seconds later, the event loop will go through another  iteration where it will now invoke the callback function and execute the console.log on line 3  (console.log('File data is',data);) here.
- This callback pattern is good, but limited and it introduces some complexities and inconveniences.
- one famous inconvenience about callbacks is the fact that we need to nest them inside each other if we're to make asynchronous actions that depends on each other.

        const fs = require('fs');
        fs.readFile(__filename, (err,data)=>{
            console.log('File data is',data);
        });
        console.log('TEST');
        
        TEST
        File data is <Buffer 63 67 6f 6e ...>
        
        
- EX #3: callback nesting

- This problem is famously known as the pyramid of doom (callback hell).
- it's make the code harder to write, read and maintain.


      const fs = require('fs');
      fs.readFile(__filename, (err,data) => {
        fs.writeFile(__filename + '.copy', data, cb2(err) => {
            // Nest more callback here...
        });
      });
    
- EX #4: promisify


- util is module in nodejs.
- promisify is a method in util module,  It is basically used to convert a method that returns responses using a callback function to return responses in a promise object.


        const fs = require('fs');
        const util = require('util');

        const readFile = util.promisify(fs.readFile);

        async function main(){
           const data = await readFile(__filename);
           console.log('File data is', data);
        };

        main();

        console.log('TEST');
        
        TEST
        File data is <Buffer 63 67 6f 6e ...>
 
 
- EX #5: fs promises 
- like ex#4 but we use native promises in fs module.  


        const {readFile} = require('fs').promises;

        async function main(){
           const data = await readFile(__filename);
           console.log('File data is', data);
        };

        main();

        console.log('TEST');
        
        TEST
        File data is <Buffer 63 67 6f 6e ...>
        
        
        
- EX #6: promise nesting

        const fs = require('fs').promises;

        async function main(){
           const data = await readFile(__filename);
           await fs.writeFile(__filename + '.copy',data);
           // more awaits here
        };

        main();

        console.log('TEST');
        
        TEST
        File data is <Buffer 63 67 6f 6e ...>
        
---

## Event Emitters:

- events library, we don't install any thing just require it, which is built-in.
- we usually name the result of requiring the events library the EventEmitter class. 
- is one of most important built-in libraries in node becuase most of the other modules implement the EventEmitter module.
- For example, streams in Node are event emitters. 
- stdin and stdout are both streams (process.stdin, process.stdout) 

- EX #1:
- in this example console.log invoked 0 times, the reason is order. we subscribed to the TEST_EVENT three times, but that TEST_EVENT fired after we subscribed to it.
- it was emitted once before we subscribed to it, but no one was listening at that point. 

        const EventEmitter = require('events');

        const myEmitter = new EventEmitter();

        myEmitter.emit('TEST_EVENT');

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });


- EX #2:



        const EventEmitter = require('events');

        const myEmitter = new EventEmitter();

        myEmitter.emit('TEST_EVENT');

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });


        myEmitter.emit('TEST_EVENT');

        // result:
        
        TEST_EVENT eas fired
        TEST_EVENT eas fired
        TEST_EVENT eas fired
        
- EX #3: event loop to trigger subscriber's callback functions happend after it without moving it to after the subscribe calls.

- the callback of setImmediate will be placed on the event loop, and it will be invoked after the rest of this program is executed.
- so the three subscribe calls will happen before the emit call in that case, and we see the TEST_EVENT was fired message.

        const EventEmitter = require('events');

        const myEmitter = new EventEmitter();

        setImmediate(() => {
          myEmitter.emit('TEST_EVENT');
         });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        myEmitter.on('TEST_EVENT', () => {
          console.log('TEST_EVENT eas fired')
        });

        // result:
        
        TEST_EVENT eas fired
        TEST_EVENT eas fired
        TEST_EVENT eas fired  

----

## Working with Web Servers:

- first calss citizen meaning we can pass functions as arguments to other functions.
- higher order functions those are functions that receive other functions as arguments or return other functions.
- response, request objects are streams.
- the request object is a readable stream.
- the response object is a writeable stream.

----

## Node web framworks:

- `npm init --yes` is command will create a package.json file.
