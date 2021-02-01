# Command Line Arguments

## Definition:
Strings of text used to pass additional info to a program when an app is run through the command line interface

--

## Syntax:
`$ [runtime] [script_name] [argument-1 argument-2 argument-3 ... argument-n]`
* Runtime = anything that exectues a program or script
* Arguments are usually separated by a space, but some can also use commas depeneding on runtime used

--

## Passing Command Line Arguments in Node.js with `process.argv`
* Built-in method in Node.js
* Global object that you can use without importing any additional libraries
* Pass arguments to a Node.js application, and you can access them within the application via the `process.argv` array

### Syntax of Array
* **First element** (index 0): always a file system path pointing to the `node` exectuable
* **Second element** (index 1): name of the JavaScript file that is being executed
* **Third+ element** (index 2 onward): first arguement actually passed by user

#### Tips: Remember JS uses zero-based indexes on arrays

### Example
Use following JS codes in new file `processargv.js`
```javascript
'use strict';

for (let j = 0; j < process.argv.length; j++) {
    console.log(j + ' -> ' + (process.argv[j]));
}
```

Run command in Terminal
```
$ node processargv.js tom jack 43
```

Output:
```
0 -> /home/vagrant/.nvm/versions/node/v14.15.4/bin/node
1 -> /vagrant/w1/d1-focal/processargv.js
2 -> tom
3 -> jack
4 -> 43
```

--

## Using the minimist Module
* minimist module will parse arguments from the `process.argv` array and tranform it into an easier-to-use **associative array**
  * access the elements via index names in addition to the index numbers
