---
layout: post
title:      "Providing Feedback to the User"
date:       2019-12-16 04:41:23 +0000
permalink:  providing_feedback_to_the_user
---


I've been working on a travel stats app called "Oh the Places I've Been!". While designing it, I initially focused on its functionality. For example, if I click a button, does the app correctly complete the task of the button. I soon realized that it was important for the user to immediatly know if the button worked. In my app, the buttons were working, but the user couldn't see that unless they scrolled down the page. To increase the ease of use of the web application, I added feedback messages to let the user know that the app had responded when they pushed a button. I used two visual cues to let the user know the button click was successful. I removed the button and I added a success message.

An overview of this travel app can be found in my previous posts about [React Hooks](https://marie-burns22.github.io/react_hooks_building_a_travel_stats_app) and [Javascript Objects in React State](https://marie-burns22.github.io/javascript_objects_and_react_state).

### Feature: Add Country to List Buttons 
Two buttons allow the user to add a selected country to a list of countries they have traveled to, or a list they want to travel to.

### Problem: Missing feedback to user
The buttons both functioned correctly, but the user had no immediate feedback on the part of the screen visible on most devices. The user had to scroll down the page to see that the country was added to the appropriate list.


### Solution Part 1: User sees a message that the country was successfully added to the list.

This project uses [react-bootstrap](https://react-bootstrap.github.io/getting-started/introduction/) for basic styling. One component included is a [Toast](https://react-bootstrap.netlify.com/components/toasts/#toasts), which pops up a message in response to an event. I use two toasts in this app to give the user feedback when they click the buttons to add a country to a list. Either they get a message that the country is already on a list or a sucess message that they have now added it. In the following example. the state and the`addToMyCountries` function are in App.js, but the buttons and toast are rendered by other components receiving props.

To implement a toast, use React state and the State hook:

```
const [showA, setShowA] = useState(false);
```

Then declare a function to toggle the state:
```
const toggleShowA = () => setShowA(!showA);
```

This function is then called when the user tries to add a country to a list and the country is already on a list. 

```
const addToMyCountries = () => {
    let onLists = checkLists();
    if (onLists) {
      toggleShowA();
    } else {
      setMyCountries(myCountries => [...myCountries, selectedCountry]);
      addToLanguages(selectedCountry.languages);
      toggleShowC();
   }
  }
```

It toggles the state for `showA` to `true` which then renders the toast because the `show` property is now set to `true`:
```
<Toast show={props.showA} onClose={props.toggleShowA}>
  <Toast.Header>
	<img className="rounded mr-2" alt="" />
	<strong className="mr-auto">{props.selectedCountry.name} is already on your list.</strong>
 </Toast.Header>
</Toast>
```

### Solution Part 2: Remove the buttons

When the button is clicked and the page rerenders to show the updated list, both buttons are removed. They both reappear when a new country is selected from the list. 

Implementation:  The rendering of the buttons is set as a conditinional based on the same state that determines if the toasts show. If any toasts are set to show, then the buttons do not render.  The following code is from the `Forms.js` component that renders the region and country select inputs then uses the props passed from `App.js` to determine if the app should render a toast or the two buttons:

```
{(props.showA || props.showB || props.showC) 
                ? 
                <Toasts 
                    selectedCountry={props.selectedCountry} 
                    showA={props.showA}
                    showB={props.showB}
                    showC={props.showC}
                    toggleShowA={props.toggleShowA}
                    toggleShowB={props.toggleShowB}
                    toggleShowC={props.toggleShowC}
                
                /> 
                : 
                <Buttons 
                    selectedCountry={props.selectedCountry}
                    addToMyCountries={props.addToMyCountries}
                    addToWantToVisit={props.addToWantToVisit} 
                />
                }
```

In the above snippet, if any of the `show` state are true, then the `Toasts` component is rendered and will show the appropriate toast. If none of them are true, then the Buttons component will render and show both buttons.













