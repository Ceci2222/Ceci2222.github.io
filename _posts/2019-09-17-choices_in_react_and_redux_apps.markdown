---
layout: post
title:      "Choices in React and Redux Apps "
date:       2019-09-17 18:48:50 -0400
permalink:  choices_in_react_and_redux_apps
---

Building an app using React and Redux gives a developer a lot of flexibility and choices in how to organize the components and pass objects between those components.  When learning React and Redux it can be confusing to determine when you have choices and when code needs to be a specific way.  To help sort this out, I've created a list of the common choices that the developer can consider throughout the development of the app.  For each, there is not a wrong answer. Any choice should work (as long as you code it correctly) and the decision comes down to the specific functions of the app and developer preference. For example, one developer may prefer to never use a local state while another developer may decide to use it for specific tasks such as storing form data until the form is submitted.  For all these choices there is no need to treat the option as one or the other.  Within the app you can use  props from both routes and from connect, both functional and class components, and both local state and store.  You can also code most of your routes in one container and then selectively move some to other components when it makes sense.


## Props from  `Route` or props from `connect` and `mapStateToProps`?

#### **Using Route**
You can pass props to a component using a Route. Here is an example of an `App.js` component that passes props using `mapPropsToState`.  Ccode not directly relevant the example is removed and BrowserRouter is implemented in and passed down from Index.js.

*  The prop `services`  comes from the redux store.  The services in the store are fetched by a `componentDidMount`lifecycle function and added to the redux store using an action creator and reducer.
*  `mapStateToProps` and `connect` make `services` available in props. 
*  The `<Route path='/services'...../>`  renders the `Services` component with `services` as a prop.

* In the `<Route path="/services/:name....../>`  the component `Service` is rendered with a prop named `service` 
* `service` is set by calling a `findService()` function (which also uses the `services` provided by `mapStateToProps`).

```
//App.js

import React from 'react';
import { Route, withRouter } from 'react-router-dom';
import { connect } from 'react-redux'
import {fetchServices} from './actions/serviceActions'

import Service from './serviceComponents/Service'
import Services from './serviceComponents/Services'

class App extends React.Component {

  componentDidMount() {
    this.props.getCurrentClient()
    this.props.fetchServices()
  }
  
  findService = (serviceName) => {
    const services = this.props.services
    return services.find(service => service.attributes.name === serviceName)
  }

  render () {
    return (
      <div>
         <Route path='/services' render={routerprops => <Services {...routerprops} services={this.props.services} />}  />
         <Route path="/services/:name" render={(rprops) =>  <Service {...rprops} service={this.findService(rprops.match.params.name)} /> } />
      </div>
    );
  }
}

const mapStateToProps = state => {
  return {
    services: state.services
  }
}

export default withRouter(connect(mapStateToProps, {fetchServices})(App));
```

The `Service` component uses the props passed from `<Route path="/services/:name" render={(rprops) =>  <Service {...rprops} service={this.findService(rprops.match.params.name)} /> } />`  by calling `props.service`.  The example `Service` component below shows that these props are avialable without using `mapStateToProps` or `connect` within the component itself.  Since this is a functional component, the props will be passed in as an argument.


```
// Service.js

import React from 'react';

const Service = (props) => {
 
    return (
        <div className="card">
            {props.service 
            ? 
                <React.Fragment>
                    <h3>Service: {props.service.attributes.name}</h3>
                    <h4>Category: {props.service.attributes.category}</h4>
                    <h4>Price: ${props.service.attributes.price}</h4>
                </React.Fragment>
            : 
            null}
       
        </div>
    )
}

export default (Service)

```



#### **Using `mapStateToProps` and `connect`**

The class component `App.js` above shows how `mapStateToProps` can be used with `connect` to set props.  The `findService` function shows the use of props. Since this is a class component, the props are not passed in, but instead called using `this.props`. This same functionality could have been implemented in the `Service` or `Services` components to set the props directly in those components, however, I chose to combine those tasks at the  `App.js` level and pass them down.



## Functional or class component?

It would be possible to write all components as classes. However, you can shorten and simplify the code by writing functional components instead.  The most important reasons that would require a class component is the need for a local state or lifecycle functions.  



## State versus store?
The Redux store makes it more convenient to pass in props to any component. It is also easy to use the Redux dev tools to see your store change instantly.  Local state can be useful if you have information that is temporary and only used in one component. For example, changes in forms before submitting the form.  By keeping this information in local state you do not have to worry about action creators, reducers, or making sure that props are rendering the most current information in the store.
