---
layout: post
title:  "Creating an app with Preact, Typescript and Parcel"
date:   2020-05-16 15:28:54 -0300
categories: development
tags:
  - js
  - development
  - nodejs
---

If you have been coding in the JS ecosystem for a while you're probably familiar
with Webpack and React, but this post is not about them :troll:
Instead this post is about creating an app with [Preact](https://preactjs.com/),
[Typescript](https://www.typescriptlang.org/) and [Parcel](https://parceljs.org/).

### But, why?
Good question, the reason because I've chosen these tools is because I wanted a lightweight
app without too much configuration (that's why Parcel and Preact) and I wanted to dive into
the static checking and typing world that Typescript provides. And plus to those reasons I'm
a developer, I like trying new technologies and having an opinion with a background to
support it.

### Let's get into the technology
First we need nodeJS, I like to use [asdf version manager](https://github.com/asdf-vm/asdf).  
Install [asdf nodeJS plugin](https://github.com/asdf-vm/asdf-nodejs.git): `asdf plugin-add nodejs`

Now we can go ahead and create the app folder:  
`mkdir your_app`  
`cd your_app`  
`npm init`  

With `npm init` we'll get two important files, `package.json` and `package-lock.json`. These files will
contain the dependencies.

Add parcel, preact and typescript to the dependencies:   
`npm i typescript@next preact parcel-bundler ts-loader --save`.

Your `package.json` will look similar to this:  
```json
{
  "name": "your_app",
  "version": "1.0.0",
  "description": "",
  "main": "y",
  "scripts": {
    "start": "",
    "build": ""
  },
  "author": "you",
  "license": "ISC",
  "dependencies": {
    "preact": "^10.4.1",
    "ts-loader": "^7.0.4",
    "typescript": "^4.0.0-dev.20200514"
  },
  "devDependencies": {
    "parcel-bundler": "^1.12.4",
    "sass": "^1.26.5"
  }
}
```
The `package-lock.json` will get auto populated, don't edit it directly.

#### Typescript config
You will need a tsconfig.json to indicate typescript configuration :  
```json
{
  "compilerOptions": {
    "outDir": "./dist",
    "sourceMap": true,
    "noImplicitAny": true,
    "module": "es6",
    "moduleResolution": "node",
    "target": "es6",
    "jsx": "react",
    "jsxFactory": "h"
  },
  "include": ["./src/**/*"]
}
```
This file indicates you have a `dist` folder for the compiled files and `src` folder for the source files, so don't forget to create those folders (or use the names you like).


#### Parcel config
You will need an index.html entry point:
```
<!doctype html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport"
      content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Your App Name</title>
  </head>

  <body>
    <div id="root"></div>
    <script src="src/index.tsx"></script>
  </body>

</html>
```
In this file the src for the script is the main file in your src folder, in my case `src/index.tsx`.

And we need the parcel scripts to start and build our app, in `package.json` in the scripts section add:
```json
"scripts": {
    "start": "parcel index.html",
    "build": "parcel build index.html"
  },
```

#### Sample files
We need a HelloWorld component, src/HelloWorld.tsx:
```js
import { h, Component } from 'preact';

export interface HelloWorldProps {
  name: string
}

export default class HelloWorld extends Component<HelloWorldProps, any> {
  render(props) {
    return <p>Hello {props.name}!</p>
  }
}
```
And we'll use that in our src/index.tsx main file:
```js
import { h, render } from 'preact';
//import './styles.scss'; //if you have styles
import HelloWorld from './HelloWorld';

render(<HelloWorld name="world" />, document.querySelector('#root'));
```

Now we are ready to hit `npm start` and have our app displayed on the browser.




	


