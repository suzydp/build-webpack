# Z magazine

this is built with webpack for the first time to learn how to build environment

## How to build environment for webpack

### 1. Setup fundamental environment

1. npm init
```
$ npm init -y
```

2. install webpack and webpack cli
```
$ npm i -D webpack webpack-cli
```

3. create 2 files and add code for testing webpack
```
/src
├── index.js
└── sub.js
```

index.js
```
import { Hello, hello } from './sub';

// invoke file which you imported
hello();
```

sub.js
```
export const hello = () => {
  alert("Hello, this is the playground for webpack.")
}
```

4. try `npx webpack`

`/dist/main.js` will automatically generate and appear alert below:
```
WARNING in configuration
The 'mode' option has not been set, webpack will fallback to 'production' for this value. Set 'mode' optionto 'development' or 'production' to enable defaults for each environment.
You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/concepts/mode/
```

5. modify package.json
```
{
  "scripts": {
    "build": "webpack --mode development" // to invoke as 'npm run build'
  },
  "devDependencies": {
    "webpack": "^4.29.0",
    "webpack-cli": "^3.2.1"
  }
}
```

6. try `npm run build`

`/dist/main.js` will automatically generate again.
in that files, `sub.js` will integrate to `index.js`. when you executed `/dist/main.js` in HTML file, bundled code will execute.

### 2. bundle CSS

### Why bundle CSS?
Webpack can deal with every resource as the modules, not only JS but even in CSS, SCSS, img, woff, TS and so on.
Loader needs to prepare if you want to exchange with files except JS.
bundle could be faster than reading pure CSS files thanks to request is much less than reading pure JS files.

1. `npm insall` like below: (this process is continuing from the last fundamental one)
```
npm i -D webpack webpack-cli style-loader css-loader
```

2. write code on webpack.config.js
```
module.exports = {
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.css/,
        use: [
          // these loader below will execute by REVERSE order
          // + style loader - CSS will apply by inserting <style> which dynamically generated by webpack
          'style-loader',
          // + CSS-loader - @import or url() will convert to require() in JS.
          { 
            loader: 'css-loader', 
            options: {url: false} 
          },
        ],
      },
    ]
  },
}
```

3. prepare import `style.css`

