---
layout: post
title:      "Using `.include()` to speed up your Rails app"
date:       2020-03-02 04:05:26 +0000
permalink:  using_include_to_speed_up_your_rails_app
---


I was interviewing for a Ruby on Rails roles and asked to think about how to speed up page loads when rendering long lists in the view.  In this situation the index view rendered a list that included information from objects accessed with a `belongs_to` relationship.  There are multiple ways to get this information on the page. I will show two ways that differ in their speed due to the number of calls to the database. I've changed the example from what was in the interview.

In this example there are two models: teacher and student. The relationship is that the teacher `has_many` students and  each student `belongs_to` a teacher. Additionally, each teacher and each student has an attribute of `name`.

In the student index view there is a list of each student (listed by last name) and the last name of their teacher. The basic code for this (ignoring styling) looks like:
```
<% @students.each do |student| %>
   <%= student.name, student.teacher.last %>
<% end %>

```

Initially the index action in my students controller looked like this:
```
def index
   @students = Student.all
end
```

During an interview I was shown that I could decrease calls to the database by using `.include()` when assigning the value to the instance variable in the controller:
```
def index
   @students = Student.all.include(:teacher)
end
```

In the first example, the database would be accessed for each teacher name slowing down the page load. In the second example with `.include()` the database would only be accessed once because the teacher object for each student would be included in the call to assign the value to the instance variable.

This was a good example of how interviews can be a great way to learn new concepts.
