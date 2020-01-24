---
layout: post
title:      "30 days of Vanilla Javascript (Days 1 - 2) "
date:       2020-01-04 22:03:24 -0500
permalink:  digging_into_vanilla_javascript
---


I've become comfortable building React web applications, but decided that to be a better developer I need to sharpen my Vanilla Javascript skills. Several software engineers have recommended Wes Boss's [Javascript30 ](https://javascript30.com/)course and I started it Friday, January 3, 2020 with the Javascript Drum Kit project. To help retain knowledge from the projects, I am recording three ideas from each project in a weekly blog post until I complete all 30. 

### Javascript Drum Kit Project - Day 1
#### Friday, January 3, 2020
* Javascript program structure - React has a lot of files, but to get a basic Javascript app running you just need an html file and a css file will add the styling.
* Javascript html file structure - 

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Name of application</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
// all the html elements go here
<script>
// all the functions go here
// the event listeners go at the bottom

</script>

</body>
</html>

```

* `this` is important in functions to make sure actions are taken on the correct elements.

### CSS + JS Clock - Day 2
#### Saturday, January 4, 2020

* You can set the style without a css file.  The CSS can go in a style tag:

```
<body>
  <div>
   //elements
  </div>

  <style>
   htlm {
    background: blue;
    background-size: cover;
    font-family: 'helvetica neue';
    text-align: center;
    font-size: 10px;
   }

   body {
    // more styling
   }

  </style>
  <script>
   //functions go here
  </script>
 </body>
```

* You can select specific elements using `.querySelector()` and set them to a variable. This goes in the script tag. 

Example: `const secondHand = document.querySelector('.second-hand');`

* You can change the style of the selected element using a function in the script tag.

Example: 

```
function changeHand(){
   secondHand.style.transform = 'rotate(90deg)';
}
```
