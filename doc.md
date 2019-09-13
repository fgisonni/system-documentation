# Checkout System Infrastructure:

The reason for the two different templates, is because both they both have different use cases based on their builds for their respective integration setup.

## BuyGoods:

### Library:
Webpack

Unless integrated with react, won’t be able to use components. Maybe something to consider

### Technology
- @babel/core
- @babel/plugin-syntax-dynamic-import
- @babel/plugin-transform-runtime
- @babel/preset-env
- babel-core
- babel-eslint
- babel-loader
- babel-minify-webpack-plugin
- babel-plugin-transform-runtime
- babel-polyfill
- babel-preset-es2015
- babel-preset-stage-0
- brotli-webpack-plugin
- clean-webpack-plugin
- compression-webpack-plugin
- css-loader
- eslint
- eslint-config-airbnb-base
- eslint-plugin-import
- file-loader
- gzip-loader
- html-loader
- html-webpack-plugin
- mini-css-extract-plugin
- node-sass
- optimize-css-assets-webpack-plugin
- postcss-import
- postcss-loader
- postcss-nested
- postcss-preset-env
- postcss-reporter
- sass-loader
- style-loader
- ts-loader
- url-loader
- webpack
- webpack-cli
- webpack-dev-server
- webpack-merge

### On Build:
Creates multi page website.

### Future Folder Structure:
```
src/
|- app.js
|-assets/
|   |-images/
|- js/
|   |-main.js
|-pages/
|   |-m(mobile)/
|      |-billing
|      |-shipping
|      |-index.html(packages)  
|   |-d(desktop)/
|      |-billing
|      |-index.html (packages and shipping form)
|-css/
|   |-exclusive/      This folder is for all styles exclusive to components and pages
|      |-form.scss
|      |-packages.scss
|      |-(other page/component exclusive styles)
|   |-main.scss     For all global styles and helper classes - all exclusive folder styles are imported into this folder
```        

### Redirect JS
```
const redirectURL = '/m'
if((navigator.userAgent.match(/iPhone/i)) || (navigator.userAgent.match(/iPod/i))) {
   if (document.location.pathname.indexOf(redirectURL) == -1) {
       document.location.href = redirectURL;
   }
}
```
______________________________

## In House:

### Library:
Preact

With Preact we can create a reusable component library, to help make maintenance easier. Create fast web app when site is built.

### Technology
- eslint
- eslint-config-synacor
- jest
- jest-preset-preact
- less
- less-loader
- per-env
- preact-cli
- preact-cli-plugin-netlify
- preact-render-spy
- webpack

### On Build:
Create single page (progressive) application.

### Future Folder Structure:
```
src/
|-offer.json
|-assets/
|   |-images/
|   |-icons/
|-components/
|   // All folders contain index.js file
|   |-footer/
|   |-header/
|   |-products/
|- routes/
|   |-m(mobile)/
|      // All folders contain index.js file  
|      |-packages
|      |-billing
|      |-shipping
|   |-d(desktop)/
|      // All folders contain index.js file  
|      |-shipping
|      |-billing
|- style
|   |-exclusive/      This folder is for all styles exclusive to components and pages
|      |-form.less
|      |-packages.less
|      |-(other page/component exclusive styles)
|   |-main.less     For all global styles and helper classes - all exclusive folder styles are imported into this folder
```
# File Setup

## Style:
Uses Less CSS compiler to manage and handle page styles
All routes of the design will be styled through all the css coded in the LESS files.

### SASS
```
/*
  Sugar Balance Naming & Colour Variables
*/
$sb: sb
$sb-bg: #ccc;
...
```

### LESS
```
/*
  Sugar Balance Naming & Colour Variables
*/
@sb: sb
@sb-bg: #ccc;
...
```

***Mixins will be added upon development***

## offer.js:
This file will be used to handle content specific to each offer type. With dynamic rendering we can pass content through string compilation using curly braces. By following the json string path, we can easily change the look of the template. For example:


### offer.js - template example:
```
{
  offer: [{
    sugarBalance:[
      selector: ‘sb’,
      productName: 'Sugar Balance',
      proceedButtonText: 'Procceed to Shipping',
      shippingButtonText: 'Procceed to Billing',
      billingButtonText: 'Pay Now',
      onePackage: '69',
      threePackage: '59',
      sixPackage: '49',
      threePackagePercentSavings: '70',
      sixPackagePercentSavings: '50'

    ]
  }]
  ...
  //Will consist same templating for different offers
}
```

### example.css:
```
.sb .background{
    background: #ccc;
}
```

### index.html:
```
<body className={ offer.sugarBalance.selector } >
```

### render build:
```
<body class=“sb” >
```

## Images:
All images in the images folder will need their offer name tied to the image file. Example:

### image:
```
sb-product-image.png
```

### index.html:
```
<img src={ offer.sugarBalance.selector + ‘-product-image.png’ }
```

For routing on different devices, can work along side router function to change the template based on screen size.
[***One solutuon***]: (https://stackoverflow.com/questions/47970343/how-to-block-a-react-route-based-on-device-dimensions)
