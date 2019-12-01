---
layout: post
title:      "React Hooks: Building a Travel Stats App"
date:       2019-12-01 15:07:30 -0500
permalink:  react_hooks_building_a_travel_stats_app
---



### Class Components to Function Components
For my previous React apps, I have mostly used class components to handle state with some Redux. For [My Travel Stats React web app, ](http://mytravelstats.netlify.com/)I am writing function components and using hooks to handle local state. I will use two React hooks to build this app. The objectives of this blog post are:

1. Encourage anyone thinking about, but hesistent to try React hooks to read the excellent docs and give them a try!
2. Show a more complex implementation of the State Hook to update an array of objects in state.

### State and Effect Hooks to Manage Data from an API

#### What is the problem My Travel Stats Web Appplication is trying to solve?
In my past life as an international school teacher, I traveled. A lot. I filled my bucket list multiple times and drained it every time. It felt gluttonous and at the same time completely normal since everyone I worked with was living the same life. But, how to keep track of all the beautiful countries I had visited? Too many to count on fingers and toes.  Counting stamps in a passport is inefficient since I lived in South Korea and they stamp your passport everytime you leave and return so half my passport was Korean stamps. Seems like a job for a React App with state. (To be clear, travel is not a competition of how many countries your visit, but stats are fun and each country on the list a little reminder of experiences and people.)

#### How are hooks used to solve the problem?
My Travel Stats is a web application that asks the user to select a country and create lists of countries they have visited and want to visit. The app uses state to keep track of the country the user has selected, the lists they have created and other stats. The app returns country statistics from an API based on user selections. The app transforms the data from the API and the user's lists to render statistics such as total countries visited. 

I used two hooks:

1.[State Hook](https://reactjs.org/docs/hooks-state.html)
* Declared multiple state variables.
* Update state when data is returned from API and based on user interaction

2.[Effect Hook](https://reactjs.org/docs/hooks-effect.html)
* Request data from an API based on user input (selection of a specific region from a drop down menu and then a country).
* Pass an optional second argument to `useEffect` so the request is only sent when the user input changes (region selected from drop down menu). Without the second argument, the request would be sent every time the page renders since `useEffect` is triggered by every render of the page.


### Beyond the docs: Example updating state when it is an array of objects

#### Problem:  Need to add an object to state and also update a value in an object
The docs for using React Hooks are excellent. They are clearly written. They show examples that compare how to declare and update state in Classes to using hooks. This is really useful to anyone who is already comfortable using state in classes. I was able to use the docs to get a basic version of my application started, but then I ran into a more complex use case in which I wanted to declare a state that was an array and then add objects to it.  I also wanted to be able to update specific values in previously added objects. And I wanted to be able to do both in one function.

#### Solution Example using State Hook
The API I used included, for each country, an array of official languages. Since languages are interesting and so are stats, I decided to add a stat that counted the total number of languages spoken in all the countries a user has visited.  Since many languages are spoken in multiple countries, the app needs to avoid counting countries twice. Also, a user can delete a country from the list (we all make mistakes sometimes) so the app needs to correctly remove languages from the count, but it can't remove a language if it is spoken in other countries on the visited list. 

To handle this, I declared a `languages` state as an empty array:
```
const [languages, setLanguages] = useState([]);
```

When a user adds a country to the their list of visited countries, a function `addToLanguages` is called and the country object is passed to it. This function has several tasks:
* Make a copy of the `languages` array from the state. We will call this `newLanguageList`
* Iterate over the array of languages for the selected country using `.forEach()`
* Check each language to see if it is already in `newLanguageList` using `.find()`.
* If the language is not included, add the language to `newLanguageList` as an object with the keys of `name` and `count`, which is initialized with a count of 1.
* If the language is already in `newLanguageList`, update its count by 1.

To avoid calling `setLanguages()` multiple times, I created a new copy of the array using the spread operator:
```
let newLanguageList = [...languages];
```

Then the function used `.push()` to add new language objects or `.splice` to remove a language object and replace it with an updated count. After all languages for the country were added or updated in the `newLanguageList`, the state was updated:
```
setLanguages(newLanguageList);
```

Here is the implemention with the state hook in a function component.  I removed other code from the component to focus on the specific example, but you can view the full component in my [GitHub repository](http://github.com/Marie-Burns22/travel-stats-ui) in the App.js file:

```
import React, { useState } from 'react';

function App() {
    const [languages, setLanguages] = useState([])
		
    const addToLanguages = (selectedCountry) => {
		let newLanguageList = [...languages]
		selectedCountry.languages.forEach(language => {
          let found = languages.find(l => l.name === language.name);
          if (!found) {
		    let newLanguage = { name: language.name, count: 1 };
		    newLanguageList.push(newLanguage);
          } else {
            found.count++
            let index = newLanguageList.findIndex(l => l.name === found.name);
            newLanguageList.splice(index, 1, found);
          }
       })
      setLanguages(newLanguageList);
    }
}

export default App;

```




















