## EJS as templating engine
```javascript
const express = require("express");
const app = express();
const PORT = 8080;

// add this line below
app.set("view engine", "ejs");
```

## `res.render()` to pass data to template using `views` directory

* Use `views` directory in project to take advantage of EJS shortcut

* EJS automatically looks inside the `views` directory for any template files that have `.ejs` extension