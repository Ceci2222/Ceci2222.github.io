---
layout: post
title:      "Breaking into Breakpoints"
date:       2019-08-13 17:46:19 -0400
permalink:  breaking_into_breakpoints
---


So if you've done some Ruby projects you probably have made friends with Pry or byebug to dig around in your code to fix bugs or better understand how your code behaves.  But now maybe you are learning javascript and it seems that you need a new friend to help you get to know the DOM better. I was recently introduced to breakpoints in the Chrome DevTools while working with a Flatiron Technical Coach and my eyes were thrown open. As a kid did you ever do the invisible ink science experiment with lemon juice where you write something on paper with the lemon juice and it looks invisible? Then you hold it up to a light and the message shows up in brown like magic (except its science, but oxidation probably sounds less interesting than magic unless you are a chemist and totally scary if you are a high school chemistry student studying for an exam). Well, using breakpoints and seeing the values in your code appear is even more exciting than the appearance of the invisible ink.  If your browser is set up like mine then they actually do show up in a brown box - just like the "invisible" ink.

I learned about breakpoints while struggling with javascript.  I'd barely started to use the cumbersome "console.log" and "debugger" and decided that learning about breakpoints was a better investment in time and infinitely more fun and interesting.  Here are a few tips to get you started using breakpoints, but make sure to watch a full tutorial. Here is a great video with example code to really help you understand the main features. [Get Started with Debugging JavaScript in Chrome DevTools by  Kayce Basques](https://developers.google.com/web/tools/chrome-devtools/javascript/)

## Tips for breakpoint beginners

* Get to know the **elements**, **console**, and **sources** tab of the Chrome DevTools. Each one is useful.
* Take some time to play around with a couple files by setting multiple breakpoints.  At first, the sources tab seems a bit overwhelming, but running through some files with breakpoints will help. Better to get familiar when you aren't frustrated with a bug.


## The sources tab - where to set and use breakpoints

* The Sources tab has 3 panes. Use them from left to right. 

1. In the first pane, use the "Page" to choose the file you want to work with.  If you are using a `.js` file you will probably need to open the "assets" directory and the filenames will look different but still identifiable.  When you click on one, you will see it display in the middle pane.

2. In the middle pane, you will see the code from the file you chose. To set a breakpoint, click on a line number. It will turn green to indicate the breakpoint. Set as many as you want! When you run the code it will pause on each line until you tell it to progress then it will pause on the next breakpoint.  Keep in mind that it won't execute the line it is paused on, so in some cases you may want to set the breakpoint on the next line. For example, if you are setting a variable and want to know its value, you need to set the breakpoint on the line after it is set.

3. Once the breakpoints are set, run your code by interacting with your app in the browser! If nothing happens in the dev tools, then your code is not hitting the break points.  If the breakpoint is hit you will see the screen greyed out, a popup will say "Paused in Debugger" with a play arrow, and the breakpoint line it is paused on will be highlighted (in my browser it is highlighted in green).  Now there are three places you can check the values in your code. First, look for popup boxes over specific words. Those will contain the values. Second, hover your cursor over any piece of code to see its value. Third, use the final pane on the right. There is a lot of information in this pane, but open the Scope to see the values in the local scope.  This is the same information in the popup info box, but in an easier to read format. Use the play button to progress through the breakpoints or turn them off when you find your bug.

## The console tab - still important
So if we aren't console.logging to find values, how is the console tab still useful for debugging?  Error messages.  The handy thing about error messages in the console tab of the dev tools is you can click on them and they will take you to the source tab and show you exactly where in the code the error was triggered. This may help determine where to try placing breakpoints.

## The elements tab -  finding the code for specific elements
Sometimes you can see an element in the browser and you know it has an issue, but can't quite remember exactly where it is in the code. Inspecting the elements to identify the specific lines of code is a quick way to identify where to set your breakpoints.  It is also handy for finding information provided by helpers (such as the id provided by form_tag) that doesn't show in your file but is in the html on the DOM.

## How is this useful for a Rails-JS project?
For my Flatiron Rails-JS project I used a mix of javascript, jquery, and AJAX to load an index page, show individual objects, and submit a form without refreshing the page on my previously created Rails app. Breakpoints were especially useful for checking the values of `this` and data that was fetched or posted to an API.
