# System Infrastructure:

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
|   |-assets/
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
|   |-exclusive/
|      |-form.scss
|      |-packages.scss
|      |-(other page/component exclusive styles)
|   |-main.scss
```        

______________________________

## In House:

### Library:
Preact

With Preact we can create a reusable component library, to help make maintenance easier

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
|   |-exclusive/
|      |-form.less
|      |-packages.less
|      |-(other page/component exclusive styles)
|   |-main.less
```

## Style:
Uses Less CSS compiler to manage and handle page styles
All routes of the design will be styled through all the css coded in the LESS files.

## offer.js:
This file will be used to handle content specific to each offer type. With dynamic rendering we can pass content through string compilation using curly braces. By following the json string path, we can easily change the look of the template. For example:


### offer.js:
```
{
  offer: [{
    sugarBalance: ‘sb’
  }]
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
<body={ offer.sugarBalance } >
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
<img src={ offer.sugarBalance + ‘-product-image.png’ }
```

For routing on different devices, can work along side router function to change the template based on screen size.
[***One solutuon***]: (https://stackoverflow.com/questions/47970343/how-to-block-a-react-route-based-on-device-dimensions)
