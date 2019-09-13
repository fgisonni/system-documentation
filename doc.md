# Checkout System Infrastructure:

The reason for the two different templates, is because both they both have different use cases based on their builds for their respective integration setup.

## BuyGoods:

### Library:
Webpack

Unless integrated with react, won’t be able to use components. Maybe something to consider

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
______________________________

## In House:

### Library:
Preact

With Preact we can create a reusable component library, to help make maintenance easier. Create fast web app when site is built.

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
      sup: ‘sb’,
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
<body={ offer.sugarBalance.sup } >
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
<img src={ offer.sugarBalance.sup + ‘-product-image.png’ }
```

For routing on different devices, can work along side router function to change the template based on screen size.
[***One solutuon***]: (https://stackoverflow.com/questions/47970343/how-to-block-a-react-route-based-on-device-dimensions)
