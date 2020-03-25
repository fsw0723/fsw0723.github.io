---
layout: post
title: "Configure webpack 4 for css files"
date: 2020-03-22 15:07:00 +0800
categories: front-end
---

Webpack is a static module bundler for modern JavaScript applications.
Css is the essential part for the JS web app. 
To configure css file bundling with webpack, here are some commonly used loaders/ plugins for you to consider.

## 1. css-loader
To resolve css files, definitely you need css-loader to resolve them.

Read more: https://github.com/webpack-contrib/css-loader

## 2. style-loader
After resolving css file, we need to inject the css into the DOM, where we can use style-loader to achieve this.

For example: 

```
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
};
```

Note that the loaders will be executed from right to left, from bottom to top.
Thus style-loader must be declared before css-loader.

Read more: https://github.com/webpack-contrib/style-loader

## 3. mini-css-extract-plugin
We may prefer not to inject css into the DOM directly but extract it as a single bundled css file,
this is where mini-css-extract-plugin helps. 
With this plugin, you can define the pathname you want to export to.

{% highlight js %}
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  plugins: [
    new MiniCssExtractPlugin({
      filename: 'css/built.css'
    })
  ],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: [MiniCssExtractPlugin.loader, 'css-loader'],
      },
    ],
  },
};
{% endhighlight%}


## 4.optimize-css-assets-webpack-plugin
This plugin helps to optimize/minimize the bundled css files.
This is useful for production environment to reduce the package size.


## 5. postcss-loader
Supporting different browsers is always a nightmare for web developers.
With post-css, you can use latest css syntax and it can help to transform to the ones that your supported browser recognizes.
Definitely, it can do a lot more besides this.

To read more: 
https://postcss.org/

This loader must be used before css-loader so that the generated css with browser prefix can be parsed via css-loader.

 

