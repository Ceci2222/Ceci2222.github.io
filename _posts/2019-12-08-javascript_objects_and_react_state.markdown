---
layout: post
title:      "Javascript Objects and React State"
date:       2019-12-08 13:20:55 -0500
permalink:  javascript_objects_and_react_state
---


I recently to built a simple travel stats app, [Oh the Places I've Been!](https://mytravelstats.netlify.com/). A description of it and how I used React hooks to implement state can be found in my blog post [React Hooks: Building a Travel Stats App](https://marie-burns22.github.io/react_hooks_building_a_travel_stats_app). In this article, I will explain how I updated an array of objects in state.

### Web Application Overview -  Oh the Places I've Been!
The app I am working with in this blog post uses data from a RESTful API, [REST Countries.](https://restcountries.eu/). This API returns data about each country in the world. The data I will be focusing on for this post is the array of official languages. Each language is represented by an object which contains several key value pairs. The key the app uses is the `name`.

The language names are used in this application for the travel stats section.  The user makes a list of countries they have visited and the app counts the number of languages spoken in all the countries and also lists the languages. Each language is only counted and listed once even if it is spoken in multiple countries. Users can remove a country from the list and the language count and list need to accurately update depending on if the language was only spoken in the removed country or spoken in other countries on the list.

### Managing the language list and count in local state with React State Hook
The [React Hooks documentation](https://reactjs.org/docs/hooks-intro.html) is excellent. If you are going to implement React Hooks, this should be your number one resource. 

I used multiple state variables, but the one I will focus on for this blog post is the `languages` state variable:
```
const [languages, setLanguages] = useState([])
```

`languages` is initially set to an empty array. Each language will be added once to the array as an object. This language object will have the keys of `name` and `count`. The value of `name` will be a string that comes from the country's language array. The value of `count` will initially be set to 1. If another country has the same language, the count will be incremented instead of a new object being instantiated.


### Updating an array of objects in state
The React documentation did not have examples of updating a state variable that is an array of objects. Therefore, I relied on the Javascript documentation to write a function that would update the array of objects.  This function, `addToLanguages(countryLanguages)` is called when a country is added by the list of countries that the user has visited. It accepts one argument, the array of languages for the added country: `countryLanguages`.

To update state, `addToLanguages()` creates a copy of the `languages` state array using the spread operator:
```
let newLanguageList = [...languages]
```

Next, it iterates over the `countryLanguages` using the [Javascript array method `forEach()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach).  The callback method passed to the `forEach()` method uses `find()` and the language name to check if it is already included in the `newLanguageList`.  

```
let found = languages.find(l => l.name === language.name);

```

The [`find()` method ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) will return first the language object with a matching name or `undefined`, if the language is not in the array. The value of `found` will be set to either the returned value.

If `found` is undefined, then a new language object will be instantiated with the name of the language and a count of 1. That object will be[ pushed](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) into the `newLanguageList` array.

```
if (!found) {
        let newLanguage = { name: language.name, count: 1 };
        newLanguageList.push(newLanguage);
```

If `found` has a value of an object, then the value of `count` in that object is incremented by 1. This is updating the `found` object, which is not mutating the one in the array.

```
found.count++;
```

This `found` language object with the updated count will be used to replace the same language object in the `newLanguageList` array that has the previous count. To do this, the index of the language is found using the [`findIndex()` Javascript array method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex). 

```
let index = newLanguageList.findIndex(l => l.name === found.name);

```

Then the index is used in the [`splice()` method](httphttps://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) to remove the old object and replace it with the`found` object that has the updated count. `splice()` is passed three arguments. the first is the index of the language to be removed. The second is the number of elements to be removed. The third is the element (updated language object) to be inserted to replace the removed object.

```
newLanguageList.splice(index, 1, found);
```

Finally, the state is updated with the new array of updated or added language objects using the `setLanguages()` which is a function to update state that was returned when `useState` was called along with the `languages` state variable.

```
setLanguages(newLanguageList);
```

The `removeLanguages()` function is called when a country is removed from the list and updates the `count` value to keep track of which languages should be included on the languages list in the stats section:

```
const removeLanguages = (languagesToRemove) => {
    let newList = [...languages];
    languagesToRemove.forEach(language => {
      let foundLanguage = newList.find(l => l.name === language.name);
      foundLanguage.count--;
      let index = newList.findIndex(l => l.name === language.name);
      if (foundLanguage.count === 0) {
        newList.splice(index, 1)
      } else {
        newList.splice(index, 1, foundLanguage)
      }
    })
    setLanguages(newList)
  }
```

All together this is what the function component will look like with the functions to add and remove languages from the language list (code not directly related to this post removed for clarity):

```
import React, { useState } from 'react';

function App() {

   const [languages, setLanguages] = useState([]);

   const addToLanguages = (countryLanguages) => {
    let newLanguageList = [...languages]
    countryLanguages.forEach(language => {
      let found = languages.find(l => l.name === language.name);
      if (!found) {
        let newLanguage = { name: language.name, count: 1 };
        newLanguageList.push(newLanguage);
      } else {
        found.count++;
        let index = newLanguageList.findIndex(l => l.name === found.name);
        newLanguageList.splice(index, 1, found);
      }
    })
    setLanguages(newLanguageList);
  }
	
	const removeLanguages = (languagesToRemove) => {
	  let newList = [...languages];
    languagesToRemove.forEach(language => {
      let foundLanguage = newList.find(l => l.name === language.name);
      foundLanguage.count--;
      let index = newList.findIndex(l => l.name === language.name);
      if (foundLanguage.count === 0) {
        newList.splice(index, 1)
      } else {
        newList.splice(index, 1, foundLanguage)
      }
    })
    setLanguages(newList)
  }
}

export default App;

```

Notes:
* `findIndex()` can not be replaced by `indexOf()` because it needs to accept a function in order to match to a value of a key. `indexOf()` is more useful when the array is not of objects.
* `.map()` returns an array so is not a comparable subsutitute for `.forEach()` since we want to change an existing array rather than return one.

