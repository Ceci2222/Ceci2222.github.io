---
layout: post
title:      "When Faker just doesn't fake it"
date:       2019-06-23 06:06:35 +0000
permalink:  when_faker_just_doesnt_fake_it
---


Seed data is essential for building and testing any application that will collect or organize any data. There are several ways to generate seed data quickly to test your application without spending a lot of time creating data. The Faker gem is great for this and I used it initially when I started building my Food Emissions Log application for my Flatiron Rails Project. However, once I got the basic forms, views, routes, and controller actions working, I found that the Faker data not only generated unbelievable data (which was still entertaining and useable), but I needed specific values for some attributes in order to add features such as scope methods and dropdown menus on forms with specific options.  

When I made a similar application for my Flatiron Sinatro project, I used the [Mockaroo](https://mockaroo.com/) website to generate a set of seed data and decided to try it again for this version of the application. Mockaroo can take a little more time to set up than the Faker gem, but the main advantage is that you can create a custom list of values for a field.  

For my application, the most important data collected was greenhouse gas emissions. For the emissions table there is a column for amount (float) and a column for unit (string) that together represent the greenhouse gas emissions for a specific food.  I chose to identify four specific units that could be chosen for the following reasons:

1. To standardize the data to make it more easily compareable.
2. To clearly display the emissions data in a table.
3. To sort the data based on the unit.

I also wanted to categorize the foods and limit the options for food categories to avoid duplicates or categories that were too similar.  Here is an example of the foods index that shows how the categories and units are displayed:

![Imgur](https://i.imgur.com/S1Lh1zm.png?1)



The data generated was still entertaining with foods such as Musk Ox and "Shichimi Togarashi Peppeers" which were categorized as "Egg".  However, the data generated matched the options I had included for the units and categories. The [tutorials](http://www.youtube.com/playlist?list=PLKMZcxOsC3u0Y-4CHg5SDpVjTcrvGttTt) on the Mockaroo website are helpful.  The custom option is easy to add. Just choose "Custom List" as the type and then enter the options seperated by commas.

![Imgur](https://i.imgur.com/FyOH5f6.png?1)


To set up belongs_to relationship and a join table, create a "schema" for any model that will have a foreign key. Download that schema as a CVS file and then upload as a data set. Then you will be able to choose "data set column" for a type and choose the appropriate model (dataset). See the student_id and food_id in the example above to see what those settings look like.

Once the schemas are set up and the foreign keys set, you download a JSON file for each schema with the number of rows that you choose.

![Imgur](https://i.imgur.com/B0KcE9c.png)

To set up your seed file, use the `.create!` method on each model and pass in the array of generated data copied from each JSON file.

![Imgur](https://i.imgur.com/QxLzPmw.png?1)

One other advantage to using Mockaroo is that you can see all the generated data directly in the seed file and easily check that it will work for your application.




