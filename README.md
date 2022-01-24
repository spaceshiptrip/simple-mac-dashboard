# simple-mac-dashboard
Create a very basic dashboard - work in progress

This will utilize mac commands:
```
system_profiler SPSoftwareDataType
```

Output example:
```
Software:

    System Software Overview:

      System Version: macOS 11.6.1 (20G224)
      Kernel Version: Darwin 20.6.0
      Boot Volume: Macintosh HD
      Boot Mode: Normal
      Computer Name: takamine
      User Name: Torres, Jay (US 397P) (jtorres)
      Secure Virtual Memory: Enabled
      System Integrity Protection: Enabled
      Time since boot: 2 days 8:42

```

And shortcut:
```
sw_ver
```
Output Example:
```
ProductName:	macOS
ProductVersion:	11.6.1
BuildVersion:	20G224
```



# Simple Docker Express Application

NOTE: This needs updating

This is a simple example of a dockerized express web application.  It returns a message when the root location is hit.  

## Install

1. Build Dockerfile:
   ```
   docker build -t simple .
   ```
   
## Execution
1. Run Dockerfile:
   ```
   docker run -d -v ${PWD}:/app -v /app/node_modules -p 8080:3000 --name foo --rm simple
   ```
   
## Usage
1. Test with cURL command:
   ```
   curl -i localhost:8080
   ```
1. Open browser to `http://localhost:8080`


## More Info
#### Docker
The Docker run command:
```
docker run -d -v ${PWD}:/app -v /app/node_modules -p 8080:3000 --name foo --rm simple
```
* -p 8080:3000
   * This redirects 8080 from your browser or external application to the container's port 3000 because the application is listening on port 3000
* --name foo
   * This is the simple name for the container, you can stop it with:
   ```
   docker stop foo
   ```
* --rm simple
   * This is the name of the container you built from the first command


#### Server code
The code is doesn't serve any static page to make it really easy for an HTTP response:
```
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!! From your Simple Express Web-Server!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

If you wanted to server a static page, use another simple express code:
```
// just server the local directory
var connect = require('connect');
var serveStatic = require('serve-static');
var port = 8080;
connect().use(serveStatic(__dirname)).listen(port, function(){
        console.log('Server running on ' + port + '...');
});
```
This serves the local directory 
Be sure your `package.json` contains this dependency:
```
  "dependencies": {
        "connect": "3.x"
  },
```
  

h1. DEBUG
```
docker run -it --rm  --entrypoint sh simple
```

That will get you in the container shell and you can run the app manually to see the error message:
```
# docker run simple
```


## ADDED this comment for zsh

