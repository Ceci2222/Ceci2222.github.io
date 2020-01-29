---
layout: post
title:      "30 Days of Vanilla Javascript (Day 17 - 24)"
date:       2020-01-26 17:32:20 -0500
permalink:  30_days_of_vanilla_javascript_day_16_-_18
---


During the past couple of weeks I have been reading and thinking a lot about habits and habits versus will power. This all ties into goals, priorities, and productivity. When I started the Javascript30 course I wanted to form a new habit and I was able to stick to one lesson a day for twelve days in a row! Daily situations changed for the two weeks after that and I have found myself scrambling to make up multiple lessons in a day. As I write this I am several days behind. After the momemtum and consistency of those first twelve days it feels like a failure to not complete one lesson a day for thirty days, but I decided to take a wider view of the situation. I considered where this goal and habit of one lesson per day fit among the many long term and short term priorities as well as my desire to develop good habits. When I look back on the days that I didn't do the lessons, I am able to see that there were other priorities and accomplishments that were more important. The goal of this course is to improve my Javascript skills and I am still on track to do that. As I balance competing priorities over the next week I will see if I can complete the 30 lessons in 30 consecutive days or if I will adjust the habit to meet the goal and all the other goals I am excited to work towards.

### CSS Text Shadow Mouse Move Effect
#### Lesson 16, Day 22: Friday, January 24, 2020
* ES6 Destructuring constants. Example without destructuring:
```
const width = box.offsetWidth;    // box is an html element that was selected with a querySelector and assigned to the variable name box.
const height = box.offsetHeight;
```
Same variables using destructuring:
```
const { offsetWidth: width, offsetHeight: height } = box;
```


* `this` versus `event.target` in callback function: In the callback function on an event listener, `this` will always refer to the element the event listener is assigned to. However, event listeners can be triggered by child elements of it. `event.target` is the element that triggered the event, which can be a child of the element the listener is assigned to. Therefore, `this` and `event.targer` may not have the same value. This can be useful.
* A CSS attribute can have multiple versions simulaneously. For example, text can have multiple `textShadows` that are set in a callback function: 
```
text.style.textShadow = `
    ${x}px ${y}px 0 purple,
    ${x * -1}px ${y * -1}px 0 green
 `;
```

### Sorting Band Names without articles
#### Lesson 17, Day 24: Sunday, January 26, 2020
* [Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)  - takes a callback that compare two elements at a time. You can call other functions in this block to transform the passed in data before you compare it. For example, in this lesson, we wrote a function that removed the articles (a, an, the) and called that on each string passed into the callback of the sort function. This allowed us to sort the strings without the articles.
* Regex - `^()` the caret looks for whena string starts with what you put in the parenthesis.  `i` at the end of the regex signifies that it is case insensitive.  Example: `/^(a |the |an)/i` will look for lower or uppercase a , the, and an.
* If you have a function in your file that you have not called in the script, you can test it without using console.log. Make sure your file is saved and running in the browser and then just call the function in the dev tools console. Why do I always forget basic tricks like this??
* Also, don't forget how useful `.innerHTML` is for adding text to an element from a variable. This works for mapping over an array of elements and diplaying them in `<li>`s.

### Tally String Times with Reduce
#### Lesson 18, Day 24: Sunday, January 26, 2020
* When you create a variable using `document.querySelectorAll()` the value is not an array even though it appears that way in the console. It is a nodeList and a nodeList does not have the same built in methods as an array. That is why if you try to use `.map()` you will get an "is not a function" error. However, in the console you can see the methods available to a nodelist in its `__proto__: Object` dropdown attribute. I think I wrote about this before, but its important and I had forgotten so its worth noting again.
* Use `Array.from(document.querySelectorAll('an attribute goes here'));` to make the nodelist into an array. You could also use the spread operator.
* You can use `.map()` with `parseFloat` to change all elements in an array from strings to numbers: `array.map(parseFloat)`
