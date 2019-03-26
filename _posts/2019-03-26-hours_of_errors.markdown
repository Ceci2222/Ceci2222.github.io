---
layout: post
title:      "Hours of errors"
date:       2019-03-26 04:49:56 +0000
permalink:  hours_of_errors
---


>We must not say every mistake is a foolish one.  ~ Cicero

>But some mistakes sure feel exceptionally foolish.  ~ Marie Burns


Error messages.  When you first start coding they look like gibberish.  Then you can pick out a little useful information. Then they start to make more sense. Finally, they become the leading guide for tracking down all the little things you broke. Or rather, the code you wrote broken.  Your confidence rises as you pinpoint line 28 of the application controller as the cause of those red lines of error messages and your browser telling you "Sinatra doesn't know this ditty..."

Several hours later, you have the same error message and Sinatra still isn't singing.  Maybe days go by. You ask for help and share the error message, and the specific code you are sure is the problem, with a friendly technical coach. Still stuck.  Eventually, in a hidden corner of the application you thought was unrelated to your line 28 error message, you find that extra line of code, or the wacky params, or that one capitalized letter that shouldn't be. And you feel foolish. You feel exceptionally foolish because it took a screen share with a technical coach to unbury it. The TC is always very kind and reassuring that these little mistakes happen to everyone including them.  But still, those hours of errors sometimes feel like a house of horrors or comedy of errors.

When the zoom meeting ends, you have a minute to sit and realize that you probably spent several hours trying to rewrite code that was actually functional because you didn't think about how every line of code is somehow related to every other line of code in the application. Line 28 was just the first step in the investigation, it wasn't the real problem. By not taking a drone level view of the situation you can completely miss the errors that led to line 28 failing the test.

After all this time and foolishness,  I have reflected and made a list of the forgotten corners to check for little mistakes before I spend hours trying to rewrite those methods that might not be the real problem. The list is somewhat organized by the level of frustration.

**Look for the details**
* params - check all the params to see what information is being passed in from all forms
* schema - check that the schema is correct including the spelling of each column and the data type
* extra lines of code that you may have because you've been copying and pasting from your notes of example code (watch out for the form inputs)
* autocorrect capitilize in all the wrong places, but specifically in the name fields of your forms.
* name fields of forms must match column titles exactly and be the correct data type


**Dig in from every angle and get all the information before you mess with your code.**
* shotgun it
*  tux it
*  rspec it
*  pry it from the console
*  pry it from shotgun  

**Read Ahead**

If you have directions, read ahead, make sure you understand all the parts.  Even if you are working one test error at a time to build the code in a methodical way, check for any methods later on that might not allow tests to pass early on. For example, if there is a flash method near the end of the lab directions, you may need to add it to get earlier tests to pass if they are looking for a specific message to flash on the screen.

**Know you are less foolish now than before**

Even though I wish desperatly to not waste so much time on little errors like these, I always come away with new knowledge and a bit of satisfaction.  In having to thoroughly inspect every line of code in every model, view, and controller, I really learn what each line does.  When I screen share with a technical coach, I have to practice explaining the code and collaborating to problem solve.  And finally, the more hours and days it takes to get all those green lines of passing code to stream through the terminal, the more exciting and satisfying the victory is.

