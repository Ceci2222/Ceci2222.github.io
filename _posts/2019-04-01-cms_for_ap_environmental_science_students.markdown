---
layout: post
title:      "CMS for AP Environmental Science Students"
date:       2019-04-02 02:20:22 +0000
permalink:  cms_for_ap_environmental_science_students
---


### **Background**
I teach AP Environmental Science for high school seniors in east San Jose, CA.  One project students complete is called a Personal Impact Project in which they collect data on their own greenhouse gas emissions and then use data they research online to analyze and compare how different changes to their daily habits could redice their greenhouse gas emissions.  Each student chooses to focus on greenhouse gas emissions from their transportation, household appliances, or diets.  

### **Challenge**

After facilitating this project a couple years, I have found that online data emission data for transportation and applicances are  pretty easy for students to find online. For transportation, students generally study about four cars and public transportation. For home electricity use, students often choose several types of lightbulbs, or about five appliances.  However, students who choose to study diet often spend a lot more time tracking down data for all the different foods that they use. Though there are several useful websites with greenhouse gas emissions, none include all the foods a student needs. 

### **Solution**
For my Flatiron Sinatra Project, I created a basic content management system (CMS) for students to collect and share greenhouse gas emission data for food.  In this basic version of the application, all students can see the list of foods with their emissions that have been entered.  Students who create an account and are logged in, can create new food entries, edit their previous entries, or delete their entries.  Each entry includes the source of the data so that it be can verified.  The end goal is that while the project is in progress, the CMS is a way for students to collaborate and research data more efficiently.  A teacher may use the same list from one year to the next, or choose to start a new one each year so that students gain experience researching data and evaluating the credibility of sources.


### Project Process
#### Sinatra
This dynamic Ruby web application was built using Sinatra. The benefits of using Sinatra in terms of writing the application are that it provides methods to build routes using HTTP requests so that students can request and fill out forms or views of data.  In terms of learning web development, it helped me better understand the basic concepts of Rails.  

#### MVC
This is a Model View Controller Application. It has a student model and a food model.  Both models have views that display their information and provide forms to create and update information.  There are three controllers, the application controller, the student controller, and the food controller.  This follows the principle of single responsibility.  One could argue that there could also be a session controller, however, I chose to assign session responsibilities to the student controller.

#### ActiveRecord and CRUD
To persist the information entered by students, I used Active Record and implemented all four CRUD functions.

##### *Create*
Each model can create new instances that are saved as objects.  The student model instances are created by the sign up form while the food instances are created by the new food form that logged in students can access.

##### *Read*
The read function is used to view a list of all the food data that students have entered and well as a page that lists each student contributor and the entries they created.

##### *Update*
A logged in student can update their food entries to correct errors or update with more accurate information.

##### *Delete*
A logged in student can delete their food entries. They may do this if they see that another student has added duplicate information or if they determine that their entry is not credible.

### **Limitations**
#### *Teacher Accounts*
This application currently does not create teacher accounts. For use in a real classroom, there would need to be a moderator to check that information added was appropriate and accurate.  If a teacher model was added, then each student would "belong to" one teacher and each teacher would "have many" students.  The teacher would also have the option to preview and approve all entries before they are visible to everyone.

#### *Units and Conversions*
There are a variety of units for emissions used by different souces. To make this application more student friendly, it would include a page explaining the different ways that emissions are measured and also allow students to complete the conversions in the application.


### Future Thoughts
I've been a teacher for twelve years, so when thinking of problems to solve with web applications, my students are what dominate my thoughts. This is the second application I have written with the focus of data research for my environmental science students for projects that I will never teacher again because I am changing careers. However, I see two purposes in continuing to write programs for my students. First, I will be handing my classroom room and curriculum off to my current resident teacher (often called a student teacher). If I am able to turn these mini projects into fullly functioning applications, they would be very useful to her and her future students. Second, as I think about future career paths, it seems that years of experience as a user of edtech would be valuable when designing and improving applications for students and teachers.  These projects have been good practice in identifying challenges and then thinking through how to code a solution with a specific user in mind.










