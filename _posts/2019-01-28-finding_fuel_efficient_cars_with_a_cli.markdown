---
layout: post
title:      "Finding Fuel Efficient Cars with a CLI"
date:       2019-01-29 02:02:44 +0000
permalink:  finding_fuel_efficient_cars_with_a_cli
---


**Choosing information for the CLI**

I teach Environmental Science and often ask my students to use data that they find online. We are currently studying greenhouse gas emissions so I wanted to write my project using one of the websites I use with my students.  In the CLI gem project I chose to scrape fueleconomy.gov to look at data for the top 8 most fuel efficient cars for 2019. There is a lot of information on this website so I chose the most relevant for a first and second level scrape.

**Running the CLI**
The CLI starts by listing the top 8 fuel-efficient cars in a numbered list. This list comes from a scrape that passes the information to the Car class where objects are created of each car.  The list collects the model attribute (name of car) from the car objects.  It then asks the user to select a car using the numbers on the list to get more information about one  car.  The user gets back a list of attributes that were added to the car object when it was instantiated. 

Next, the user is asked if they would like additional information.  If they select yes, then the second scape method is called using a url that goes to a page that gives information about the selected car.  This url was also added to the car object when it was created. After the additional information is listed, the user is asked if they would like to select another car. If they input yes, then they run through the program again. If they select no, then they exit the program.

**Reflection on the process of creating the CLI**
Creating this project was fun.  One aspect that was rewarding was getting the program to work as intended and then reviewing it to figure out how to refactor it to improve it. The most important refactor that I did was with the responsibilities of the scrape and CLI controller modules.  I realized after it was working, that I had given the second scrape method the responsiblity of listing information for the user.  It worked in this program because there was very little information to return. However, this isn't really the responsibility of the scraper so I moved that job to the car class.  I also realized that the CLI controller had some methods that really should be in the car class such as listing the car information.  The start method also contained too many responsibilities that I refactored into other methods.  

**Reflections on the CLI**
As currently written, the program scrapes for several attributes of each car. If this was a longer list of cars, it might make more sense to only intially scrape the model attributes and then when the car is selected, scrape for the additional attributes of that car to add to the object.  Also, the program could provide another menu of information options such as MPG and ask the user which specific information they would like, then scrape for that specific information. However, the list of cars is short and the scrape runs quickly. 


The fueleconomy.gov website has mutliple tabs of information on the page with the range and cost. It would be interesting to figure out how to access those additional tabs with the CSS selectors so more information such as emissions could be added to the information options.
