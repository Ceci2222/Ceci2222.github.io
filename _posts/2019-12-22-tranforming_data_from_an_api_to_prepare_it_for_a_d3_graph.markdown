---
layout: post
title:      "Tranforming data from an API to prepare it for a d3 graph"
date:       2019-12-22 19:43:11 +0000
permalink:  tranforming_data_from_an_api_to_prepare_it_for_a_d3_graph
---


In a recent code challenge, one of the tasks was to create a d3 bar graph of data retrieved from the YouTube API. In this blog post I will explain the following steps:
* Use the controller to return a JSON formatted endpoint
* Use the d3 fetch module to retrieve the data from the json endpoint and transform it into an object of the data to be rendered.

### Controller
In the controller action (usually the index or show), use the `respond_to` block to return the data as a json object.  The json endpoint can be viewed in the browser by appending `.json` to the end of the url. For example, when running this program on my local server, I can view the json object at `http://localhost:3000/page.json`

```
class PagesController < ApplicationController
  
	def show
    _ids = search[:items].collect{ |i| i[:id][:videoId] }
    @videos = get_full_details(_ids)["items"]

    respond_to do |format|
      format.html
      format.json { render json: @videos }
    end
		
  end
end
```

### Graph.js

I created a javascript file that would take the json data and render it as a graph. 

`d3.json()` comes from the [d3-fetch module](https://github.com/d3/d3-fetch/tree/v1.1.2). This can be installed with `npm install`. It takes an argument of an endpoint. Then you pass it a function that transforms the data to create an array of objects that will be rendered in the d3 graph. In this example, the array is declared with `const movies = []`.

`.forEach` interates over each element in the data. It creates a new object for each element, and pushes the new object in to the array.  Because it is json, the data types of the values will be strings and numbers will need to be changed to integers with `+` (shorthand for parseInt()). The new objects will just include the key-value pairs needed for the graph and ignore the other data. 

Finally, `render()` function is called with the new array (movies) passed in. This function will create the graph. 

```
///
$(document).ready(function () {
    graph();
});

var graph = function () {

    d3.json("/page.json").then(data => {
        const movies = [];

        data.forEach(d => {
            let movie = {};
            movie["title"] = d["snippet"]["title"];
            movie["viewCount"] = +d["statistics"]["viewCount"];
            movie["likeCount"] = +d["statistics"]["likeCount"];
            movies.push(movie);
        });
        render(movies);
    });
    
    const render = movies => {
        ... //This function uses the json object created above to render a d3 graph.
    }; 
};
```


