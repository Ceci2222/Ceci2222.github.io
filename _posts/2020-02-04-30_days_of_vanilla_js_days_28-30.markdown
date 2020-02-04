---
layout: post
title:      "30 Days of Vanilla JS (Days 28-30)"
date:       2020-02-04 23:29:18 +0000
permalink:  30_days_of_vanilla_js_days_28-30
---


These notes are the last of the lessons for Wes Bos's fabulous [Javascript30](https://javascript30.com/) course. 

### Stripe Follow Along Dropdown
#### Lesson 26, Day 28: Thursday, January 30, 2020
* You can select just the direct descendents of an element. This is useful if you are trying to avoid many levels of nested elements. For example, if you have nestes `li`s you can just grab the first level by selecting the `li`s of the parent class (such as the class of the `ul`). Example: `const triggers = document.querySelectorAll('.cool > li);`
* Arrow functions and `this`!  If you put a function in a block, `this` is not inherited, except if you use an arrow function.  If you  use an arrow function then the value of `this` is inherited. 
* You can change the CSS property of an element with `.style.setProperty('nameOfProperty', value)` For example: 

```const background = document.querySelector('.dropdownBackground');
background.style.setProperty('height', `${coords.height}px)`);```

### Click and Drag to Scroll
#### Lesson 27, Day 28: Thursday, January 30, 2020
* To see multiple values with the variable names in the console, put the variables in an object in the console.log: `console.log({x, startX});`
* Using `e.preventDefault();` whenever you pass an event into a function, protects against the browser carrying out any unexpected or undesired actions.
* I was struggling to really understand`scrollLeft` so I looked it up on the [MDN Javascript Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollLeft). `Element.scrollLeft` is a property of an element object and is provided by the Web API of which `Element` is a one type of object that provides an interface (Still learning how to use all the terms so that statement might not be totally accurate).  This is a value you can get or set. However, it seems that the element needs some CSS in order to change the value from 0:  `overlfow-x: scroll;`

### Video Speed Controller UI
#### Lesson 28, Day 29: Friday, January 31, 2020
* You can call .`querySelector()` on more than just document. You can use it on an element you have already selected and assigned to a variable. Example: `const bar = speed.querySelector('.speed-bar');`
* It is very useful to keep remembering that when you use an event selector, the event and `this` are not the same. I am not sure why I keep forgetting. It is helping to console.log each of those when I add an event selector as a visual reminder that each of them is very useful because of the API that provides all the attributes for each of them.
* `.toFixed(1)` can be called on a number to set how many decimal places are displayead. Example: `bar.textContext = playbackRate.toFixed(1) + 'x';`
* There are many attributes of specific types of elements that are built in such as `video.playbackRate` that you can set.

### Countdown Clock
#### Lesson 29, Day 29: Friday, January 31, 2020
* Date has a static method you can use to get the current date and time that you can use like this: `const now = Date.now();`
* To make a variable available the entire window you can set it as a global variable outside of any function. By declaring it with `let` you can then assign and update its value in other functions while still having it available throughout the application.
* `setInterval()` and `clearInterval()` are both methods provided by the Web API on the `WindowOrWorkerGlobalScope` mixin which provides features those two interfaces(Window interface and the WorkerGlobalScope interface). Other methods in the same mixin include `setTimeout()` and `clearTimeout()`. More details in the [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope).

### Whack A Mole
#### Lesson 30, Day 30: Saturday, February 1, 2020
* Example of uses of recursion: in a function to choose a random number, you can prevent the same number from being returned twice in a row by using recursion to call the function again if the number is called twice. You can also use it to repeated run a function until a condition changes.
* Events have an `isTrusted` attribute that can be used to check that events are real and not faked by Javascript.  
* The combination of `setTimeout()` and `remove()` are useful for animations since you can specify an amoun of time that a class is added to an element. 

