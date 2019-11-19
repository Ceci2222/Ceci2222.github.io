---
layout: post
title:      "ActiveAdmin, Create-React-App, Heroku, Netlify, Ruby on Rails - Part 2"
date:       2019-11-18 10:41:14 -0500
permalink:  activeadmin_create-react-app_heroku_netlify_ruby_on_rails_-_part_2
---


This article describes how to deploy a create-react-app to Netlify.  It includes steps to connect the app to a Rails backend that is hosted on Heroku.  You can follow [Part 1](https://marie-burns22.github.io/activeadmin_create-react-app_heroku_netlify_ruby_on_rails_-_part_1) for one way to set up the Rails API with an Active Admin dashboard.


---

### Step 6- Set up cors in Rails app so frontend can call backend
1. In your Rails app, Add `gem 'rack-cors' to Gemfile.` Make sure to `bundle install` it.
2. In `cors.rb` uncomment out the block and add in the origins for your development and production apps. The example is setup for an app that does not require any login by the frontend user. <script src="https://gist.github.com/Marie-Burns22/9a2380482845b0ff6d6f47db5ebf66ae.js"></script>
3. Push these change to Heroku from the terminal command line: `git push heroku master `.



### Step 7- Create-React-App
1. Make a new React app in a separate directory from the rails app. For example, you make have one project directory named `project` and within it two app directories: `/project/project-backend` (where you rails app is) and `/project/project-frontend` (for the React app). To make the React frontend app, follow the directions in the official [Create React App guide](https://create-react-app.dev/docs/getting-started/). 
2.  Create a repository on Github and connect your React app to it.
3.  This guide will not cover how to make a React app.
4.   You can use various [libraries](https://reactjs.org/docs/faq-ajax.html#example-using-ajax-results-to-set-local-state) to make API calls to your rails backend. Just check that the urls you use include both the current heroku app name/url and the correct name-spacing set up in your rails routes.  Example: `https://dcpr.herokuapp.com/api/v1/teachers`  not `https://dcpr.herokuapp.com/teachers` if you put your controllers in the `/api/v1` directory with corresponding routes.

### Step 8- Deploy to Netlify
1. Create a Netlify account. 
2. Find the button/option for "New Site from Git". 
3. Make sure your current directory is your app's root directory and then run in the terminal command line: `npm run build` . 
4. At some point you will need to allow Netlify access to your Git repository. You can either allow it access to all your repositories or add them one at a time as you create sites.
5. There will be a page that allows you to set your "Build Settings".  If you used create-react-app, set "Build Command"  to  `npm run build`  and  "Publish directory" to  `build/`. 
6. Follow the [Netlify docs](https://www.netlify.com/blog/2016/07/22/deploy-react-apps-in-less-than-30-seconds/) to add a redirect rule if you used routing in your React app.
7. Change the site name. If you have a custom domain name or want to buy one from Netlify, go to "Domain Settings". If you want a free name (will still contain 'netlify') but want to choose it, go to "Site Settings", "Site Information" and click the "Change Site Name" button.

8. Any changes pushed to the master branch of your git repository will be deployed. There are directions in the Netlify docs to change the branch if you prefer.
 


---
