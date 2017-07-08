# webpack-css-bundle-example
> Transform SASS and bundle the base style + styles from used components.

## Component A

JS
```javascript
import './component-a.scss';
  
export default function ComponentA() {
  console.log('A');
}

```

CSS
```scss
@import 'vars';
  
.a { color: $main-color; }
```

## Component B

JS
```javascript
import './component-b.scss';
  
export default function ComponentB() {
  console.log('B');
}

```

CSS
```scss
@import 'vars';
  
.b { color: $secondary-color; }

```

## Index (entrypoint)

JS
```javascript
import './index.scss';
import ComponentA from './component-a';
  
ComponentA();
```

CSS (index.scss)
```scss
@import 'vars';
  
body { font-family: $base-font; }
```

CSS (_vars.scss)
```scss
$main-color: red;
$secondary-color: blue;
$base-font: 'Roboto', sans-serif;
```

## Webpack config

```javascript
const path = require('path');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve('dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [{
      test: /\.scss$/,
      use: ExtractTextPlugin.extract({
        fallback: 'style-loader',
        use: ['css-loader', 'sass-loader']
      })
    }]
  },
  plugins: [
    new ExtractTextPlugin('styles.css'),
  ]
}
```

## Result (bundle)

CSS
(Component B styles are not present)
```css
body { font-family: "Roboto", sans-serif; }
.a { color: red; }
```
