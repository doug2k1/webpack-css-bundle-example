# webpack-css-components

## Component A

JS
```javascript
import './component-a.css';
  
class ComponentA {
  render () {
    console.log('A');
  }
}
  
export default ComponentA;
```

CSS
```css
.a { color: red; }
```

## Component B

JS
```javascript
import './component-b.css';
  
class ComponentB {
  render () {
    console.log('B');
  }
}
  
export default ComponentB;
```

CSS
```css
.b { color: blue; }
```

## Index (entrypoint)

JS
```javascript
import './index.css';
import ComponentA from './component-a';
  
const myA = new ComponentA();
myA.render();
```

CSS
```css
body { margin: 0; }
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
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['env']
        }
      }
    }, {
      test: /\.css$/,
      use: ExtractTextPlugin.extract({
        fallback: 'style-loader',
        use: 'css-loader'
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
```css
body { margin: 0; }
.a { color: red; }
```
