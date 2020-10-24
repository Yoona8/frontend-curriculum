# Node.js
<details>
<summary>Installation and basics</summary>

- install node.js
- run the file in terminal
```bash
node <file-name.js>
```
- uses modules (add via `require`)

</details>

<details>
<summary>File access</summary>

- comes with node, no need to install
```JavaScript
const fs = require('fs');

// file is created relative to the current path
fs.writeFile('user.txt', 'user=Harry', error => {
  if (error) {
    console.log(error);
  } else {
    console.log('Success!');
  }
});

fs.readFile('user.txt', (error, data) => {
  if (error) {
    console.log(error);
    return;
  }

  console.log(data);
  console.log(data.toString());
})
```

</details>

<details>
<summary>Working with http requests</summary>

- run the file
- open in the browser
```JavaScript
const http = require('http');

// to config a server
http.createServer((request, response) => {
  let body = [];
  
  // GET / - for the first load of the page
  // POST / - if we add the form and submit it
  console.log(request.method, request.url);
  
  // parsing the data (incoming)
  request.on('data', (chunk) => {
    body.push(chunk);
  });

  request.on('end', () => {
    body = Buffer.concat(body).toString();
    console.log(body); // => user="Harry"

    // to set headers
    response.setHeader('Content-Type', 'text/html');

    // simple text
    response.write('Hello!');
    // or html (ex: form)
    response.write(`
      <form method="post" action="/">
        <input name="user" type="text">
        <button type="submit">Send</button>
      </form>
    `);
    // will send the response
    response.end();
  });
// to run a server
}).listen(3000);
```

</details>

<details>
<summary>Express.js</summary>

- easier way to deal with http requests
- install to dependencies
- set a bunch of functions to deal with the requests (works like a middleware), works with the same response
- package for parsing the response body `body-parser`
```JavaScript
const express = require('express');
const app = express();
const bodyParser = require('body-parser');

app.listen(3000);

// adds the parsed body to request object
// in the next middleware function
app.use(bodyParser.urlencoded({extended: false}))

app.use((req, res, next) => {
  res.setHeader('Content-Type', 'text/html');

  // if we're not done with the response
  // goes to the next function
  next();
});

app.use((req, res, next) => {
  const userName = req.body.user || 'Unknown';
  // send is an express method
  res.send(`<h1>Hello ${userName}!</h1>`);
  // don't use next if we're done with the request
});
```

</details>

<details>
<summary>Rendering Server-side HTML with Template and EJS</summary>

```bash
npm install --save ejs
```
```JavaScript
// set the engine for parsing our template to ejs
app.set('view engine', 'ejs');

// set path to folder with templates
// templates should have the ejs ext
app.set('view', 'views');

app.use((req, res, next) => {
  const userName = req.body.user || 'Unknown';

  res.render('index', {
    // data to use on a view
    user: useName
  });
});
```

</details>

<details>
<summary>Basic REST routes with Express.js</summary>

```JavaScript
// app.js
const express = require('express');
const bodyParser = require('body-parser');
const router = require('./routes/location');

const app = express();

app.use(bodyParser.json());
app.use(router);

app.listen(3000);
```
```JavaScript
// routes/location.js
const express = require('express');
// import for using features, not for server creation

const router = express.Router();

const locationStorage = {
  locations: []
};

// works like a middleware, but for a specific method and url
router.post('/add-location', (req, res, next) => {
  const id = 1;

  locationStorage.locations.push({
    id,
    address: req.body.address,
    coordinates: {
      lat: req.body.lat,
      lng: req.body.lng
    }
  });

  // the same as with res.send(); but already specified json
  res.json({
    message: 'Successfully stored!',
    locationId: id
  });
});

// dynamic segment of the link = :id
router.get('/location/:id', (req, res, next) => {
  const locationId = req.params.id;
  const location = locationStorage.locations.find(location => {
    return location.id === locationId;
  });

  if (!location) {
    return res.status(404).json({message: 'Location not found!'});
  }

  res.json({
    address: location.address
  });
});

module.exports = router;
```
- sending the request
```JavaScript
// front-app.js
fetch('https://localhost:3000/add-location', {
  method: 'POST',
  body: JSON.stringify({
    address: 'Some address',
    lat: 10,
    lng: 10
  }),
  headers: {
    'Content-Type': 'application/json'
  }
})
  .then(response => console.log(response));

// getting the current query params from the link address
const locationId = queryParams.get('location');
fetch(`https://localhost:3000/location/${locationId}`)
  .then(response => console.log(response));
```
- CORS (Cross-Origin Resource Sharing) - by default browsers block such requests
- always configured on backend with setting the headers
```JavaScript
// app.js

// ...

app.use(bodyParser.json());

app.use((req, res, next) => {
  // '*' any other server
  // or specific URL
  res.setHeader('Access-Control-Allow-Origin', '*');
  // options because before sending POST req
  // some browsers first send OPTIONS request
  res.setHeader('Access-Control-Allow-Methods', 'POST, GET, OPTIONS');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type');
  next();
});

// ...
```

</details>