---
layout: post
title:      "ActiveAdmin, Create-React-App, Heroku, Netlify, Ruby on Rails - Part 1"
date:       2019-11-12 12:23:32 -0500
permalink:  activeadmin_create-react-app_heroku_netlify_ruby_on_rails_-_part_1
---


This article describes the steps I have used to create a basic application using Ruby on Rails API, an ActiveAdmin dashboard and Create-React-App. There are many ways to get a website up and running for a small business, but here are the reasons that I chose these technologies:

**Ruby on Rails API only with ActiveAdmin**  -  Fast way to get an API setup to store the information that will be displayed on the website. ActiveAdmin is a fairly simple admin dashboard interface so the client can create, edit, and delete information displayed. 

**Create-React-App  **-  Quick way to get a React application started.

**Heroku**  -  Easy and free or cheap to host the API.
**Netlify**  -  Easy and free to host the frontend.

Part 1 of this blog will cover setting up a Ruby on Rails API with an ActiveAdmin dashboard and deploying on Heroku. 
Part 2 will cover deploying a Create React App on Netlify and connecting it to the Rails API.


---

### Resources
**[Heroku Docs](https://devcenter.heroku.com/articles/getting-started-with-rails6)** : Getting  started with Rails 6. 

**[A Rock Solid, Modern Web Stack - Rails 5 API + ActiveAdmin + Create React App on Heroku](https://blog.heroku.com/a-rock-solid-modern-web-stack)**  -  Blog post by Charlie Gleason.
I used some parts of this to get the ActiveAdmin dashboard setup. It sets up both the Rails app and the React app to run from the same repository on Heroku. However, I chose to put the Rails app in one repository and the React app is a second repository. This allowed me to easily deploy the Rails app to Heroku and the React app to Netlify. There are several blog posts out there explaining the advantages to this setup.

**[Netlify Docs ](https://docs.netlify.com/configure-builds/get-started/#basic-build-settings)**

---

## Steps and Example Code

### Step 1. Create the Rails App in API only mode with a Postgresql database and connect to a Github repository.


This example uses Rails 6.0.0 and Ruby 2.6.1 

Use the following command line code to create a new rails app that is api only and uses postgresql as the database.  Make sure you are in the directory you want the new project folder to be created in.
```
rails new <app_name> --api --database=postgresql
```

Change into the directory of the new app (or open in vs code and continue to run commands in the vs code terminal):
```
cd <app_name>
```

Create the database to avoid no database error.  Note: Still looking for a good resource to explain this step. The Heroku documentation and other blog guides I referenced did not include this step, but I found it necessary
```
rails db:create
```

Check that the app works by running local server. Should see "Yay! You're on Rails"
```
rails s
```

Initialize your project directory with git and connect to a github repository:
```
git init 
git add .
git commit -m "first commit"
```
Go to github and create a new repository without README (was already created by rails so there will be problems if you try to create a file in the new repository).  Then copy and paste into the command line the code provided for the option "...or push an existing repository from the command line"

### Step 2. Setup Active Admin Dashboard.

Follow directions in Step 2 from [A Rock Solid, Modern Web Stack - Rails 5 API + ActiveAdmin + Create React App on Heroku](https://blog.heroku.com/a-rock-solid-modern-web-stack#step-2-getting-activeadmin-working), except for the change below to deal with an update to Sprockets AND disregard any directions in reference to sqlite3 since we set up the app with Postgresql.

**Sprockets Error**  -  Read this before you try to install active admin in the command line. 

The [rails guide](https://guides.rubyonrails.org/asset_pipeline.html) explains about what sprockets does. ActiveAdmin uses it for assets, which is why the directions in Step 2 of the Rock Solid blog post comment it back in.

There was an update to Sprockets in the fall of 2019 which now requires a manifest.js file in the assets folder (the new version 4 of Sprockets will give an error about "Expected to find a manifest file"). With the api version of a rails app neither that directory or file exist. If you want to try to add the file, there are directions for what to put in the file on the [Upgrade Guide for sprockets](https://github.com/rails/sprockets/blob/master/UPGRADING.md#guide-to-upgrading-from-sprockets-3x-to-4x), but I opted to lock in the older version of sprockets:

In the gem file add:
```
gem 'sprockets', '~>3.0'
```


Then from the command line, bundle and update:
```
bundle update sprockets
```

You should now be able to continue following the directions in Step 2 of the Rock Solid blog post to install Active Admin.

### Step 3. Deploy to Heroku.

**Directions - ** Use the Heroku Docs starting at [Deploy your application to Heroku](https://devcenter.heroku.com/articles/getting-started-with-rails6#deploy-your-application-to-heroku) through the end (for some apps I ran into problems setting the ruby version so I skipped that part when necessary).

**Renaming app  -**  From the Heroku Dashboard, at the top of settings, you can change the name of the app. A popup will alert you of possible problems, but if you click on it there will be very easy directions for how to fix/prevent the problems.

**Possible Error -**  When you try to open the deployed app the in browser, you may get a black screen with an error: "This [heroku app name created by heroku] page can't be found." There are 2 options to fix this:

*Option 1 for ActiveAdmin* - The option I used because I wanted an admin dashboard.

1. Navigate to the admin dashboard  if you installed ActiveAdmin. Do this by  adding ```/admin``` to the end of the url and you will be directed to the the active admin dashboard login page. 
2. Change the seed file so the default admin login is available for first login in production - The seed file created when active admin was created has a default login you can use to login the first time (username ```admin@example.com``` and ```password``` for the password). In order to use this default the first time you login once deployed on Heroku, you will need to remove the end of line 8 in the ```seeds.rb``` file that says ``` ifRails.env.development?```.  I'm going to be upfront here and point out that I am not sure this is the best way to deal with this, but it worked for me. 
3. Commit and push the updated seeds file to the github repository.
4. Push the change to heroku using the command line:
```
git push heroku master && heroku run rake db:seed && heroku restart
```

*Option 2 for No ActiveAdmin* 

Refer to the Heroku docs for how to add a controller, view, and routes to display a simple welcome page to see that the app works. Later as you add models, serializers, controllers, and routes, you will have data that you can navigate to view and check how everything is working.

### Step 4- Setup the Models, Controllers, Serializers, and ActiveAdmin Resources
This step sets up all the models that will be controlled by ActiveAdmin and also rendered in the React App. Here is a brief overview of what we will use and why:

* **rails scaffold generator** (won't create views because it is in the api mode) to create the models and controllers. We will remove a lot of code from the controllers. They are not used by ActiveAdmin, but are used to receive and render JSON in response to requests from the frontend. So we will set them up to use a fast JSON serializer.

* **[Fast JSON API ](https://github.com/Netflix/fast_jsonapi)**- This will send our data from our backend to our frontend in JSON. 

* **ActiveAdmin Resources** - These models will generate the views and all the CRUD actions that will be accessed on the admin dashboard.

**Do these steps once per app**:
1. In ```config/application.rb``` , add ```config.app_generators.scaffold_controller = :scaffold_controller``` The error this fixes and and screenshots of the file are in [Step 3 of the Rock Solid App post](https://blog.heroku.com/a-rock-solid-modern-web-stack#step-3-adding-create-react-app-as-the-client). 
2. In the Gemfile, add ```gem 'fast_jsonapi'``` . Run ```bundle install``` . 

**Do these steps for each model you create:**
1. Use the scaffold generator to add a model and controller with one migration. Example: ``` rails g scaffold Article author:string content:string```. 
2. Run in the command line: ```rake db:migrate```.
3.  Create the serializer: Example ```rails g serializer Article author content```
4.  Call serializer in controllers: Example ```render json: ArticleSerializer.new(@articles)```
5.  Add active admin resource: Example: ```rails generate active_admin:resource Article```
6.  In the active admin model, uncomment or add ```permit_params```. Example: ```permit_params :author, :content```.
7.   Since we added an ApiController (see Step 2. Setup ActiveAdmin Dashboard), the controllers must inherit from it. Example: ```class ArticlesController < ApiController ```.


### Step 5 - Setup name-spaced routes and controllers
1. In the ```controllers``` directory add a new directory ```api```. In the api directory add a directory ```v1```.
2. Move controllers for each model you generate into the ```v1``` directory.
3. Namespace each controller and inherit from apicontroller. Example: ```class Api::V1::ArticlesController < ApiController```
4. Namespace routes in ```routes.rb```. Example:
5. <script src="https://gist.github.com/Marie-Burns22/90b61bf0dc29f493d8b7717a713980c6.js"></script>
6. Add, commit, and push changes to your remote Github repository.
7. Heroku push, migrate and restart from the command line:
```git push heroku master && heroku run rake db:migrate && heroku restart```
8. Open the deployed app admin dashboard and check that it works. Try creating some instances of your models. You should also be able to navigate to the namespaced urls and see a JSON object of the information you entered in the dashboard.


That's it for Part 1.  Part 2 will include setting up cors, create-react-act (briefly), and deploying to Netlify.
