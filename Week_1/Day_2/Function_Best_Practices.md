# Function Best Practices
Keep these rules in mind as you create functions.

1. Give your functions precise verb/action based names
    * avoid generic names like 'data' or 'run'
    * name functions beginning with *action* words like `createUser`, or `sendUserData`
    * be consistent with your namming conventions
    * if you're joining an existing project, observe and adapt ato any existing conventions
    
2. Use `camelCasedNames`

3. Properly indent the function code

4. Functions should focus on a single task: [returning a value or causing a side effect](https://eloquentjavascript.net/03_functions.html#h_EdyBGBF6y/). **Break function** into additional smaller functions if you find it **doing two or more things**

5. Data needed by Functions should be passed in as parameters/arguments (i.e. *local scope*) instead of being access directly (i.e. *global scope*)
    * *Why?* Functions that take in parameters are more reusable, since they are less depending on their surrounding (i.e their outer scope).