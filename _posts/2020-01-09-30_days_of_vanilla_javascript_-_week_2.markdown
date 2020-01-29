---
layout: post
title:      "30 Days of Vanilla Javascript  (Days 3 - 10)"
date:       2020-01-09 16:20:26 -0500
permalink:  30_days_of_vanilla_javascript_-_week_2
---

These are my daily notes for week two while going through Wes Bos's [Javascript30](https://javascript30.com/) class.

### Playing With CSS Variables and JS
#### Lesson 3, Day 3: Sunday, January 5, 2020

* You can create CSS variables to use in your JS. Then you can update styling with JS using the variables.  This can be done by declaring the variable on an element or the root in the style tag and setting the default values for those variables. In the example below the variables are declared on the root and the default values for base, spacing, and blur are set.

Example:

```
<style>
   : root {
	    --base: #ffc600;
	    --spacing: 10px;
	    --blur: 10px;
	 }
	 
	 // The CSS spacing varible is used to define the padding for img tags
	 
	 img {
	    padding: var(--spacing);
			}
</style>		
```


* `.querySelector()` returns a Nodelist. This may look like an array, but it is not. Arrays and NodeLists have different built in methods. You can see the list of available methods for either in the console (when you have one in the console, click on the expand arrows until you get the list).
* `data-attributes` These are made up attributes (replace attribute with the name of your choice). This allows you to declare an attributes with a custom name. Example: `data-sizing`.
*  `this.dataset` will create an object of all the data-attributes.


### Array Cardio Day 1
#### Lesson 4, Day 4: Monday, January 6, 2020
* `Array.prototype.reduce()` - the Reduce method can be used for multiple tasks such as summing integers or summing instances of elements.
* To test out code, write an html file and then run it in the live server. This gives access to the chrome devtools.
* `Array.prototype.sort() ` - pass in a function to determine which attribute to sort on and which order to sort.  

   Example: This will sort an array of objects based on the year key. The largest year will be first.

```
const sorted = array.sort((a, b) => a.year > b.year ? -1 : 1);
```

### Flex Panels
#### Lesson 5, Day 5: Tuesday, January 7, 2020
* Use `.forEach() to add event listeners`. 

Example: 
```
<script>
    const panels = document.querySelectorAll('.panel');

    function toggleOpen() {
      this.classList.toggle('open');
    }

    panels.forEach(panel => panel.addEventListener('click', toggleOpen));

  </script>
```

* `transitionend` event listener is useful for triggering a CSS change after a transition has finished.
* CSS flex is useful for dynamically sizing elements. You can nest flex to arrange within other blocks.

### Ajax Type Ahead
#### Lesson 6, Day 6: Wednesday, January 8, 2020

* You can create a Reg Expression from an argument that is passed into a function and assign it to a variable. Then that variable can be used in other parts of the code.  In the following example, the word is followed by another parameter in single quotes. The g tells it to search globally so it will identify more than once and the i insensitively (case does not matter):

```
function example(word, array) {

   const regex = new RegExp(word, 'g1' )
	 return array.include(regex)
	 
}
```


* Since I learned about the fetch API in the context of React, for some reason I thought it was specific to React. Nope, it can be used in vanilla JS. I think I often make assumptions about specific concepts being tied to certain languages or frameworks. This is a good reminder to make sure to better research the tools I use to see where they can be implemented.

* Difference between `change` and `keyup` event listeners: If you are typing into an input field, you have to leave the field (click outside of it) for the `change` event to be "heard". If you want each character typed to be "heard" then use the `keyup` event listener. 

### Array Cardio Day 2
#### Lesson 7, Day 7:  Thursday, January 9, 2020
* Useful array methods for checking values: `Array.prototype.some()` and `Array.prototype.every()`. For each, pass in a function to test for true/false. Can use ES6 and return implict values of true or false. Example:

```
const fruits = [
   {name: 'apple', color: 'red'},
	 {name: 'banana', color: 'yellow'}
]

//if there is at least one fruit with a value of "yellow" for the key color, then will return true, if not, false.
const isYellow = fruits.some(fruit => (fruit.color === "yellow")); 
```

* `console.table()`   organizes arrays of objects into a table! So much easier to read!
* `(new Date()).getFullYear() ` can be used to return the current year without hardcoding it. Also in VS Code when you are typing it will auto suggest other methods for anything you have typed.


### Fun with HTML5 Canvas
#### Lesson 8, Day 8: Friday, January 10, 2020

* You can draw on a web page using the HTML5 `<canvas>` element. The [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)  and Javascript are used to draw on this element. Example canvas element:

` <canvas id="canvas" width="800" height="800"></canvas>`

* Use `.getElementById()` to select the canvas element and then `.getContext()` to select the context where the drawing will be rendered.  

* To do the actual drawing, you will need to declare a function with a block that holds the appropriate methods acting onthe context, and add event listeners to the canvas. Use multiple event listeners to toggle the drawing on and off.  The following example is not complete, but just shows how the canvas and the context and assigned to variables and then how one of the event listeners is assigned to the canvas and how the draw function calls methods on the context:

```
<script>
   const canvas = document.querySelector('#canvas');
	 const ctx = canvas.getContext('2d');
	 
	 function draw(e) {
	    ctx.beginPath();
	    ctx.lineTo(e.offsetX, e.offsetY);
	    ctx.stroke();
	 };
	 
	 canvas.addEventListener('mousemove', draw);
</script>
	 
```


### Must Know Dev Tool Tricks
#### Lesson 9, Day 9: Saturday, January 11, 2020
* Breakpoints can be set on an element! In the dev tools, element tab, right click on an element and choose one of the options in the 'break on' option/submenu. For example, if you select 'attribute modification' then the break point will be triggered and show in the souces tab when an attribute on that element is modified. Remove it the same way you set it.
* `console.log()` is just the beginning. There are lots of way to display information in the console: `console.count()`, `console.dir()`, `console.assert()`, `console.clear()`, `console.group()` with `console.groupEnd()`, `console.time()` with `console.timeEnd()`, `console.table()` to show an table of an array of objects.


### Hold Shift and Check Checkboxes
#### Lesson 10, Day 10: Sunday January 12, 2020
* Flag variables - these are set to help identify or keep track of elements for specific conditions.  They are also like toggles and usually have a value that switches between false and true.  To change between the true and false use the bang operator: `!`. Example: 

```
let waterOn = false;

function turnFaucet() {
   waterOn = !waterOn;
   (waterOn) ? console.log("Turn off the faucet to save water.") : console.log("Faucet is off.")
}
```

* Remember to use `console.log(e)` more often to see all the information available in an event that could be useful for manipulating the DOM.
* Selecting element with inputs have a little different syntax (use of square brackets) than just class or id selector.  Example: `document.querySelectorAll('.inbox input[type="checkbox"]')`


