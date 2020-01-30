---
layout: post
title:      "30 Days of Vanilla Javascript (Days 25 - 27) "
date:       2020-01-30 02:03:50 +0000
permalink:  30_days_of_vanilla_javascript_days_25_-_27
---


Over half done! My notes from [Wes Bos's Javascript30](http://javascript30.com) class that is fun, high quality, and efficient in presenting relevant and useful concepts. If you want to practice your Vanilla JS, I highly recommend it.

### Unreal Webcam Fun
#### Lesson 19, Day 25: Monday, January 27, 2020
* You can use the browser to access media from a computer's devices. `navigator.mediaDevices.getUserMedia({video: true, audio: true})`
* The `localMediaStream`  that you get from the above code can be used in the `video.srcObject`: `video.srcObject = localMediaStream;`
*  Javascript can be used to manipute the pixels in an image or video. The can change the colors, make duplicate and ghost images, and even be used for greenscreen effect. To do this requires a solid understanding of how colors and the relationship between colors and math. 

### Native Speech Recognition
#### Lesson 20, Day 26: Tuesday, January 28, 2020
* `SpeechRecognition` can be used to capture audio from your devices microphone. I did a little research on it and found that when you create a new `SpeechRecognition` object it inherited a variety of properties and methods. The list is on the [MDN SpeechRecognition documention page](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition).
* Use`document.createElement('p')` to create a new element. In this example, a new paragraph element was created. 
* Use `appendChild()` to add additional child elements. This does not create the child element. Instead you pass in the already created element that you want to append. Example: 

``` 
let p = document.createElement('p');
const words = document.querySelector('.words');
words.appendChild(p);
```
* `.textContext` is useful for adding text to an element. Note to self: research different between `textContext` and `innerHTML`.

### Geolocation based Speedometer and Compass
#### Lesson 21, Day 26: Tuesday, January 28, 2020
* Xcode has a simulator you can use with options for not only the type of iOS device but also different scenarios such as running or driving so you can test out code that uses geolocation data.
* `navigator.geolocation.watchPosition()` provides lots of data such as speed and location coordinates.

### Follow Along Links
#### Lesson 22, Day 27: Wednesday, January 29, 2020
* The following example is a common pattern of creating an element, adding a class to it and then adding it to the body of a page.:

```
const highlight = document.createElement('span'); // This creates a new element based on what is passed in. In this example it will create a span element. It is assigned to a variable so that we can do things like add classes and append it to other elements in our JS script.

highlight.classList.add('highlight'); // This gives our new element a class of highlight.

document.body.append(highlight) // This takes the element we created and add it to the body of the document.
```

* When you want to add the same event listener to a collection of the same elements, first use `.querySelectorAll()` to grab them all as an array and assign them to one variable. Then call `.forEach()` on the array and pass in a function that assigns the event listen to each item in the array.  Example:

```
const triggers = document.querySelectorAll('a'); // collects all the a tags and puts them in an array assigned to the variable triggers.

triggers.forEach(a => a.addEventListener('mouseenter', lighlightLink)); // Iterates through each a tag in the triggers array and assigns it an event listener.
```

If you put a `console.log(this)` in the call back function of the event listener, then when it is triggered you will see the specific element that triggered the event in logged in your console.

* To get information about the size and coordinates of a specific element that you have added an event listener to, use `this.getBoundingClientRect();` in the callback function. Set it as the value of a variable and then you can access and use the specific data you need. Example:

```
const elementCoords = this.getBoundingClientRect(); 

console.log(elementCoords); // See all the information now available to you about the element that triggered the event.

highlightBox.style.width = `${elementCoords.width}px`;  // Use the information to set the style of a specific element.
```

### Speech Synthesis
#### Lesson 23, Day 27: Wednesday, January 29, 2020
* Most browsers come with speech synthesis API!  We are using an object created by `const msg = new SpeechSynthesisUtterance();`  We can push different attributes onto that utterance object.
* `speechSynthesis` is a global variable that has methods you can call on it such as `.speak(add variable with your utterance here)`. I wonder if the API changed since this video was made since I am able to run `speechSynthesis.speak(msg)` in the console (before writing additional functions to change the msg - just with text added) and hear "I love Javascript thumbs up.".  I was also able to add a working event listener to the speak button with `speakButton.addEventListener('click', () => speechSynthesis.speak(msg) )`.  I found that the [MDN list of event types](https://developer.mozilla.org/en-US/docs/Web/Events) is a great resource for creating event listeners. 
* Again, `this` is useful, this time in combination with `.find()`.  We use the `this.value` as a way to find a specific value in an array that matches a value of the element that triggered an event and assign it to the value of an object attribute: ` msg.voice = voices.find(voice => voice.name === this.value);`
* Use filter and includes together to keep items based on matching characters for part of an attributes value. `voices.filter(voice => voice.lang.includes("en"))`

### Sticky Nav
#### Lesson 24, Day 27: Wednesday, January 29, 2020
* When an element is set as fixed in the CSS, it does not take up space in the document. That means if an element is initially not set to fixed, if an event (such as scrolling to a certain point in the document) triggers a change to set that element to fixed, then the position of elements below it will change.  This causes a reflow and the elements below move into the vacated space.
* To prevent weird behavior caused by reflow we can add `paddingTop` equal to the `offsetHeight` of the navbar to the body when it scrolls to the appropriate point and then set it to zero when it is not scrolled to that point.  The function that add the `fixed-nav` class and the padding looks like:
```
function fixNav() {
   if(window.scrollY >= topOfNav) {
	    document.body.style.paddingTop = nav.offsetHeight + 'px';
		document.body.classList.add('fixed-nav');  
			// in the CSS add this class with position: 'fixed'
 } else {
      document.body.style.paddingTop = 0;
	  document.body.classList.remove('fixed-nav');
 }
```
* To hide elements you can use CSS and then update the style when events are triggered. For example, you can set `max-width:0;` and `overflow: hidden;` in the CSS file. Then add specific styling that reveals it when a class is added by an event.  Here is the CSS file example for the logo:

```
li.logo {
   max-width: 0;
	 overflow: hidden;
	 //additional attributes
}

.fixed-nav li.logo {
   max-width:500px;
}   
```
* You can not animate on `width` that is why `max-width` is used.

### Event Capture, Propagation, Bubbling and Once
#### Lesson 25, Day 27: Wednesday, January 29, 2020
* Bubbling in eventListeners - if you add an event listener to nested elements (such as several divs), then the event bubbles up through all the elements it is nested in. Clicking on a parent will not trigger the nested children. When you click on an element the browser starts a capture starts at the top/outermost level and works (ripples) down to capture each of those events, then bubbles from the bottom or innermost element that you triggered. It triggers each event in order on the way back up/out.
* Capture option: You can pass in an option of capture: true to the event listener that will cause the event to trigger on the capture down rather than on the bubble up. Example: `divs.forEach(div => div.addEventListener ('click', logText, { capture: true }));`. By default capture is false.
* If you do not want to trigger events on all the elements with bubbleup or capture, you can stop that by passing in the event to the function and then `e.stopPropagation();`.


