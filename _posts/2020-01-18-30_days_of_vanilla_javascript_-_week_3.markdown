---
layout: post
title:      "30 Days of Vanilla Javascript - Week 3"
date:       2020-01-18 19:52:04 +0000
permalink:  30_days_of_vanilla_javascript_-_week_3
---


These are my daily notes for week two (starting at day 11) while going through Wes Bos’s Javascript30 class.

### HTML Video Player
#### Day 11, Monday, January 13, 2020

* Data attributes are assigned as strings. If they are used as numbers they need to be parsed when retrieved.  Example: `video.currentTime += parseFloat(this.dataset.skip);`

* Video have many built in methods and attributes. Example include `.currentTime`, `.duration`, `.paused`, `.timeupdate`, `.volume`, `.playbackRate`.

* Inline functions can check for logic. In the following example, it will check if `mousedown` is true. If it is true, it will execute `scrube(e)`.  Example: `progress.addEventListener('mousemove', (e) => mousedown && scrub(e));`


### Key Sequence Detection(KONAMI CODE)
#### Day 12, Tuesday, January 14, 2020
* Key sequencing detection is used to trigger an action based on specific sequence of key strokes.

* `Array.prototype.splice()` can be used to keep an array from growing beyond a certain size even as new elements are pushed on. `.splice()` requires a start index. Optionally it can take in the `deleteCount`and element to add to the array. It will not add any elements if none are indicated. The return value is an array of all the deleted elements and the original array is mutated/changed. The start index can be measured from the end of the array by using negative numbers. For example, if you want the array to stay at a length of 5, set the start index to -6 and the delete count to 1. Then everytime a new element is added on, the length will go to 6, but because splice is -6 and the delete count is 1, the first element will be deleted.

* You can run functions in your script that are from another website by adding a script tag to that website and the appropriate file.  `cornify_add()` was used in this video to add unicorns when the correct sequence was typed.


### Slide in on Scroll
#### Day 13, Saturday, January 18, 2020
* Some frameworks come with a debounce function or you write your own (or find one online). A debounce function is useful with functions triggered by event listeners that may run too many times and cause performance issues. An example of this is a function called by a scroll event. To implement the debounce function, wrap it around the function called in the event listener.  It is a good idea to always debounce a scroll event. Example:
```
window.addEventListener('scroll'
, debounce(checkSlide));
```
* If you need to hide a photo before or after an event, use transform and translate in the CSS to move it off the screen  and set the opacity to 0. Example: 
```
.hidden {
   opacity: 0;
   transform: translateX(-30%);
}
```
* You can add and remove classes from elements using `.classList.add('class')` and `.classList.remove('class')` Example:
```
img.classList.add('active');
img.classList.remove('active');
```

### Object and Arrays - Reference VS Copy
#### Day 14, Saturday, January 18, 2020

* For strings and numbers, if you set a variable to a value and then set another variable to that variable, changes to the first variable will not change the value of the second variable.  Example:
```
let cookies = 5;
let brownies = cookies;
cookies = 4;
console.log(cookies, brownies) // 4, 5
```
In this example, brownies is a copy of cookies, not a reference.

* For arrays, the reference is to the entire array not the specific elements. Therefore, a change array1 will also happen in array2. Example:
```
let array1 = ['apple', 'banana', 'orange']
let array2 = array1;
array1[2] = "pineapple"
console.log(array1, array2) // ['apple', 'banana', 'pineapple'], ['apple', 'banana', 'pineapple']
```
This is an example of a reference instead of a copy. You have to make a copy of the array in order to makes changes to original without also changing the array assigned to the new variable.

In order to keep the original values of the array, make a copy of it using `.slice()` or `[].concat()` or the ES6 spread operator or `Array.from()`. Examples:
```
const array2 = array1.slice();
const array3 = [].concat(array1);
const array4 = [...array1];
const array5 = Array.from(array1);
```

* To make copies of objects there is a new spread operator for objects since the video was recorded. Example:
`let newObject = {...oldObject}`.

### LocalStorage and Event Delegation
#### Day 15, Saturday, January 18, 2020
* In the browser is an object called localStorage. You can view it by typing `localStorage` in the console of the dev tools. You can also see it by clicking on the Applications tab in the dev tools. There you can see the key value pairs of data in the localStorage. Note: Not an object. Can only store string data.
* You can add data to the localStorage with `localStorage.set('keyName', JSON.stringify(dataObject));`
* To access items in local storage you can use `localStorage.getItem('keyName');` This will return a string so to get an object you can use `JSON.parse(localStorage.getItem('items'))`




