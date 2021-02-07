---
layout: post
title:      "JavaScript Project"
date:       2021-02-07 18:43:21 +0000
permalink:  javascript_project
---


I began the process of planning my JavaScript Portfolio Project about a week before beginning the coding process. For previous projects this planning process has played an essential role in the success of my work and ability to structure my code easily. To me it feels like taking a bird's eye view to my project. When I am in the middle of coding a project I feel like (at least at this point in my software engineering journey) I have a bit of tunnel vision, and if I just dive right into it without taking the time to plan out the big picture I often get a little lost and scattered. I find it vital to take the time to create the user story for my app and the outline of how the project will be structured. I like to break this into sections. For the Javascript project I started by writing out my models and their relationships/attributes, controllers with the actions I thought I would need, routes and fetch requests I anticipated making, and an app flow diagram/description. 

Through the planning process I was able to narrow my project ideas down to the one I chose to pursue; an eco-forum web-app. The idea behind this was that I wanted to create an online space for environmental education, idea sharing, and mitigative inspiration. It was loosely inspired by Reddit, with the MVP (minimum-viable-product) being a single-page app with a feed of user-submitted Posts (with title and content) describing environmental issues and the ability for users to comment on said Post's with feedback, ideas, and general reactions to the content. This took some time to complete as gaining my bearings with creating my separate first front-end & back-end app came with a bit of a learning curve. 

I had a tough time with understanding how the backend relationship between Posts and Comments (Comments belong_to Post and Post has_many Comments) translated to the frontend portion of my project. At this point in the curriculum I am fairly comfortable with Rails and backend in general, while this JavaScript section was my first real introduction to frontend. After a couple weeks of not very DRY workarounds and mild-to-severe confusion I discovered and decided I should use serializers in my backend in order to structure the data being sent to the frontend via JSON. Once I had the serializers established in my backend and had included the relationships between Comments and Posts, it was much easier to work with the JSON data sent to my frontend from the backend. 

I find JS to be a really interesting language and the way in which it is used to create responsive and interactive web-content is very inspiring. This project made me start to feel like a real software engineer- able to navigate both the frontend and backend and the relationship between. 

I found some gaps in the JS curriculum as I was working through this project. I think there could be more content and labs related to the relationship between the backend and the frontend. Perhaps a larger backend-frontend lab with a pairing-option right before the project so that the concepts required for the project are more familiar. All in all, as with all of the projects, the JavaScript Portfolio project challenged me and pushed me to solidify my grasp on JS concepts and how the frontend and backend interact to produce interactive web-based applications. 

