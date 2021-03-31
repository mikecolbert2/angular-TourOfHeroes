# Angular Tour of Heroes
![Angular](https://badges.aleen42.com/src/angular.svg)

Simple application built from the tutorial on the Angular 11 website.  
https://angular.io/tutorial

.gitignore file created at: https://gitignore.io   

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.  


## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.


## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.


## Application prep for Heroku
Summary of instructions from here: https://itnext.io/how-to-deploy-angular-application-to-heroku-1d56e09c5147
  
 - [ ] Ensure you have the latest version of angular cli and angular compiler cli : ```npm install @angular/cli@latest @angular/compiler-cli --save-dev```  
  
 - [ ] In package.json, copy "@angular/cli”: “x.x.x”, & "@angular/compiler-cli”: “x.x.x", from devDependencies to dependencies.
 
 - [ ] In package.json, under "scripts" add "heroku-postinstall" ```"heroku-postbuild": "ng build --aot --prod"```  
 
 - [ ] Add the node and npm engines Heroku will use to run the application:  ``` node -v``` & ``` npm -v ```. Include at the bottom of package.json. 
```  "engines": {
    "node": "x.x.x",
    "npm": "x.x.x"
  }
```   

- [ ] In package.json, copy "typescript" : "~x.x.x" from devDependencies to dependencies.  

- [ ] Install Enhanced Resolve 3.3.0 ``` npm install enhanced-resolve@latest --save-dev ```  

- [ ] Install a server to run your app ``` npm install express path --save ```  

- [ ] Create a server.js file in the application root.
```
//Install express server
const express = require('express');
const path = require('path');

const app = express();

// Serve only the static files form the dist directory
app.use(express.static(__dirname + '/dist/<name-of-app-in-package.json>'));

app.get('/*', function(req,res) {
    
res.sendFile(path.join(__dirname+'/dist/<name-of-appp-in-package.json>/index.html'));
});

// Start the app by listening on the default Heroku port
app.listen(process.env.PORT || 8080);
console.log(`Running on port ${process.env.PORT || 8080}`)
```  

- [ ] In package.json, change the start command. ``` "start:prod": "node server.js" ```  

- [ ] Create a Procfile in the application root. ``` web: npm run start:prod ```