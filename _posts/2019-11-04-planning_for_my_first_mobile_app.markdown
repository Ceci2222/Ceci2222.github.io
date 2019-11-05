---
layout: post
title:      "Planning for my first mobile app"
date:       2019-11-05 02:16:39 +0000
permalink:  planning_for_my_first_mobile_app
---


#### Inspiration: AP Environmental Science Students
I've had a project from my Flatiron bootcamp waiting patiently on Github for an upgrade. I wrote the project to learn how to build an app with Sinatra and then later with Rails. Part of the program was then rendered with JavaScript. The project was inspired by my AP Environmental Science students who were studying their greenhouse gas emissions from their diets. We were using real data, but finding the correct data and then analyzing it was a cumbersome process. The app I built only addressed the first step in the process - finding the data for greenhouse gas emissions from specific foods. It didn't then provide a tool for students to track their own diets and complete the calculations. All of that we did with google sheets. This was a great way to teach students about google sheets, but in the end the complexity of the spreadsheets took a lot of time and some students got really frustrated with the long process. If the goal is to help students better analyze their own personal impact using real data and also learn about climate change, there needs to be a better tool to balance teaching students how to analyze data without creating a hurdle to learning by introducing overly complicated spreadsheets.

### Research: The stack

I've decided to take the idea for this app and use it to learn how to build a mobile app and an API. From my last couple of projects, I have learned that it is important to understand how all the technologies in your stack work together to make sure you choose those that accomplish your goals and are easy to integrate. I found a great article and as a read it I listed my initial thoughts, decisions, and questions below.

### Resource
Article from Savvy : [A Massive Guide to Building a RESTful API for our Mobile App](https://savvyapps.com/blog/how-to-build-restful-api-mobile-appp://)- Thorough article discussing all steps for planning the API. 

#### Ideas, Questions, Additional Research

* Use versioning
* Do all sorting and other similar tasks on the API not the mobile app. 
* Learn more about and implement RESTful architecture.
* Learn about reconciling offline activity if the mobile app is going to include a feature for students to track the number of servings the user eats of each food throughout the day.
* Research where to host. I have used Heroku, but there is a coursera specialization for google.
* Research authentication. Check AuthO and OAuth2.
* Research how to setup and use backend environments.
* Use PostgreSQL for the database if using Heroku for hosting. If another server is chosen, verify is PostgreSQL can be used or if another is preferable.
* Use Jira for project planning and tracking.
* Research and use a testing framework. Depends on language used.  If using Rails check what the default and create new app without testing if you choose another.
* Research if this a good project to learn Java or stick to improving Ruby skills.
* Learn how to use Postman for testing the API and API documentation.
* Use React Native since I am already familiar with React and it builds both iOS and Android apps.
* Consider using Expo for this first app. Hackernoon wrote a blog post explaining what it does.  
* Check out the CS50 mobile app development course on edX (uses React Native and Expo)
