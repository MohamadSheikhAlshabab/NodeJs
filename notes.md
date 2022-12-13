- Require : use it to depend on any library, whether this library is bulit-in one like HTTP or if it's third-party installed library.
- process.stdin.read() : use it to read from user's input. it's like prompt()
- process.stdout.write() : use it to write user's input. it's like console.log()
- process.exit() : use it to terminate the process.

### Destructuring :

- all these constants :
`
const PI = Math.PI;
const SQRT2 = Math.SQRT2;
const E = Math.E;
`
equals to :
`const {PI, E, SQRT2} = Math;`

- EX #2:
`
const circle = {
  label: 'circleX',
  raduis: 2,
 };
                                //// this is second parameter with default value and it's optional because of (={})
const circleArea = ({ raduis }, { precision = 2 } = {}) => (PI * raduis * raduis).toFixed(2);

console.log(circleArea(circle)); // 12.56

console.log(circleArea(circle, { percision : 5})); // 12.56637
  
`
- ex #3: destructuring with array
` const [ first, second, , forth] = [10, 20, 30, 40];
first // 10 
second // 20 
forth // 40
`
### Rest Operator: 

`const [ first, ...restOfItem ] = [ 10, 20, 30, 40 ];
first // 10
restOfItem // [ 20, 30, 40 ] create new array to hold the rest items of array after pop out the first element.
`

- ex #2:

`const data = {
  temp1: '001',
  temp2: '002',
  firstName: 'John',
  lastName: 'Doe',
};

const { temp1, temp2, ...person } = data;
`

### Spread Operator:
- spread one array or object into a new array or object, it's useful for copying arrays and objects, but it's shallow copy (any nested objects or arrays will be shared between these copies). 

`const newArray = [ ...restOfItem ];`
`const newObject = { ...person };`

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
- `
// function (exports, module, require, __filename, __diname){ // bulit-in hidden wrapping function
     console.log(arguments);
// }
`
- you can use exports or module.exports to define the API of a module.
- you can use require to require other modules inside this one.
- `__filename` has the path to this file.
- `__ dirname` has the path to the folder hosting this file.
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
  
        ` exports.language = "English";
          exports.direction = "RTL";
          exports.encoding = "UTF-8";
        `
        
    file2.js
   
      `
        const api = require('./file1');
        console.log(api.language, api.direction, api.encoding); English RTL UTF-8
      `
2- Top-level API is an array:

  - file1.js
  
       ` module.exports = [2, 3, 5, 7];`
       
  - file2.js

      `
        console.log(require('./file1')); // [2, 3, 5, 7]
      `
      
 3- Top-level API is a string:
 
 
  - file1.js // this file is returning a template string
  
       ` module.exports ='// this is backtick (because  is multiline template string)
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
         '
       `
       
 - file2.js
   
      `
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

            </body>
            </html>
      `
