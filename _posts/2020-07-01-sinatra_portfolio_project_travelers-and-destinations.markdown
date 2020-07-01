---
layout: post
title:      "Sinatra Portfolio Project: Travelers-and-Destinations"
date:       2020-07-01 15:27:30 +0000
permalink:  sinatra_portfolio_project_travelers-and-destinations
---



The way that models, views, and controllers work together feels very organic to me; like the ebb and flow of the ocean. This project really solidified my understanding of MVC structure and the ways in which each element works together to connect the user to the database. I began this project by brainstorming on paper how I wanted my domain model to be set up. The first step that I took was to draw out the models I planned to use, including their attributes and the relationships between them. This visual representation helped me to start to picture what the rest of my web-app was going to look like. 

The domain I chose to work with was travelers and destinations, with a user (aka traveler) being able to signup or login and create, edit or delete destinations. In my domain, a User has_many Destinations and a Destination belongs_to a User. Thus my CRUD routes were to be held within my Destinations Controller and the routes for signup, login, and logout were to be in my Users Controller.   

To start, I set up the file structure for my project. It is important to structure your folders and files in line with convention. I then setup my Gemfile, requiring the gem's I knew I would need for this project. Following, I setup my config.ru file, requiring my environment file and mounting my controllers, including Rack::MethodOverride in order to use the Update (patch route) and Delete's (delete route) of CRUD. Following this path, I then worked on my environment file; requiring bundler,  setting my connection to the database, and 'require_all'-ing from my app directory. 

After setting up these structural elements of my app, I moved on to defining my controllers and models. I made sure to follow convention in defining each of these files, and set my Application Controller to inherit from ActiveRecord::Base and my Users Controller and Destinations Controller to inherit from Application Controller. 

Within the User Controller, I defined the has_secure_password method, user-input validations for username presence and  uniqueness, as well as a validation for the presence and valid format of the user's email input. In my Users Controller I also defined the has_many :destinations relationship. In the Destinations Controller, I made sure to define the belongs_to :user relationship. 

After this, I moved on to the Application Controller, in which I defined my configure block and set views to the 'app/views' directory, enabled sessions, and set my session secret. 

It was then time to work on my migrations, which I created through the command-line and then defined my users and destinations tables within these files. 

Following this leg work it was time to work on my routes within my controllers. I began by setting up the structure for my CRUD routes in my Destinations Controller, then running shotgun and working between browser and my Destination Controller and destination views. I set up all of my routes in Destinations Controller so that it was working in browser, then moving on to my Users Controller to work on my signup, login, and logout functionality. As I set up the User routes, I moved between User Controller, user views, and updating my Destination Controller routes to include the User Controller functionality. As I worked through the User Controller routes, I defined helper methods in my Application Controller that simplified my Users and Destinations Controller code (making it more DRY), including 'logged_in?', 'current_user', 'authenticate', and 'authorize'. 


The use of pry, shotgun, and tux really helped me to understand what my code was actually doing as I was creating my routes, views, and models. I was able to identify where things were going wrong and if I was having an issue and visualize how my model relationships were set up. I found that creating my own web-based Sinatra application was easier than passing some of the labs in this section, as it was always the little spelling mistakes or spec requirements that tripped me up. In my own project I could decide what attributes, keys, and labels I was using, avoiding the tedious mistakes I have so often made in labs. 
