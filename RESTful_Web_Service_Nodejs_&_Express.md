# What is REST ?
- __RE__ presentational   __S__ tate   __T__ ransfer

----

## tools:

- ___ESlint___ : 
    - in package.json: under scripts we add `"lint" : "eslint .",` (dot is run the app and validate that we are writing our code properly )
    - in terminal: `npm run lint -- --init`
    
- ___nodemon___:


    - in package.json: 


                             "nodemonConfig":{
                              "restartable":"rs",
                              "ignore":[
                                "node_modules/**/node_modules"
                              ],
                              "delay":"2500",
                              "env":{
                                "NODE_ENV":"devlopment",
                                "PORT":4000
                              }
                               
    - if get an error process not defined:
       - add to eslintrc.js:
                               
                                  "env":{
                                    "node":"true"
                                  },
                                   "globals": {
                                      "process": true
                                    }
