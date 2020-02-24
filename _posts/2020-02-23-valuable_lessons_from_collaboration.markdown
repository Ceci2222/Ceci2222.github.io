---
layout: post
title:      "Valuable Lessons from Collaboration"
date:       2020-02-24 04:43:13 +0000
permalink:  valuable_lessons_from_collaboration
---


The past couple of months I have collaborated on a project started by another Flatiron Grad. I found his posting on our slack channel asking for collaboration for a Ruby on Rails and React web application. Having just graduated from the online, self-paced program, I was excited to jump into a project with another developer since up to that point all my experience programming was solo. Adam had built most of the Rails API only backend including testing and authentication. My task was to build the React frontend including sign up and login features.  We are almost ready to deploy!  There are many things I have learned through this experience. In this post I will share a few lessons specific to collaborating using version control versus using it solo.


#### Branching, merging, pulling
* I had to learn the order and timing of pushing commits to branches and requesting merges to the protected master. When you work alone without any protected branches (such as the master), it is pretty easy to keep track of which branches you have pushed commits to and which need to be merged.  If you work with a collaborator, there may be a protected branch. In this case you will need to take extra steps and allow time for the branch to be merged. If you forget to request the merge, or don't wait for the merge to be completed before you do a 'git pull' of the master branch, then you may overwrite the work you did. If you are lucky, you can still access the work you did from your local branch. If you are in the habit of doing a 'git pull' before you work each day, it may be helpful to check the remote repository to make sure you are pulling what you think you are pulling.
* Version control requires excellent communication skills. Everyone needs to be aware of who is working on each file. Otherwise, you will run into merge conflicts.  Messy.
* I am still sorting out how branches off of branches are seen by different collaborators. What steps do you need to go through to see a branch off a branch that someone else created.

##### Takeaways for learning how to play nicely with others using version control.
* Using version control solo is more straightforward than with a team.
* The most helpful exercise for learning version control with a team was to do a screen share and walk through creating branches, pushing, pulling, commiting and merging. We kept our remote repository open (this was on Gitlab) to see what commits and merges were visible and completed on the remote.  This was really helpful for seeing how changes we did affected the work of collaborators.


