---
layout: post
title: "OptimalPack Frontend Rebuild"
date: 2021-01-18 23:55:00 -0700
categories: programming
tags: [React.js, Flask]
thumb: /assets/images/posts/optimalpack-food.png
project: OptimalPack
---

I learned React.js by using it to build a real UI for the OptimalPack database.<!--more-->
The interface used to look like this:
![old-img]

And now it looks like this:
![food-img]

I am pretty happy with the improvements.
The rebuilding started during the week-long break between semesters, shortly after I turned the project in. I looked into React, learned a bit of how it worked, and built a preliminary test of a basic UI before my next semester started. I came back to the project months later and started over using React Hooks to keep the code cleaner. The UI project has actually been restarted three or four times now as I learned more about React, and about front-end design in general. The learning curve has been steep, but I have a clear idea of what I want and no time constraints, so I am taking the time to restart and do it right when needed.

At this point, the UI is based on _[React Table](https://www.npmjs.com/package/react-table)_, a Hooks-based, headless table plugin that can sort, filter, pivot, and as far as I can tell, do anything that I could want a table to do. The headless nature of the plugin means I can style the thing however I want, which I am sure I will appreciate eventually. The learning curve was a bit steep since the documentation was heavy on examples and light on simple explanations, but the docs were recently updated. They are much more comprehensive, but I have already spent enough time digging through the author's GitHub repo and have gotten comfortable with the library. For now, I'm really happy with how the UI is going.

![meals-img]

One issue is that the back end files are getting out of hand. The original controller used MySQL Connector to interact with the database, but writing and debugging the raw SQL got annoying very quickly. I restarted with Flask and SQLAlchemy because they are simple and easy to use, but I didn't realize I was buying in to a whole new relational model by doing so. For building the UI, I have been slowly re-implementing the database with SQLAlchemy, but my Flask file has gotten huge and unwieldy. For now I will be stepping away from this project to work with a small group on an application using Django, and will probably be making the switch from Flask to Django once I have gained a little more experience. I have also tried to keep all of the table functionality in one (large) component while controlling the specifics of each table with header files. We will see if that is still a good idea when I come back to the project. For now, I am just happy that I have a working prototype for my frontend. With a little styling, it might even start to look nice.

[food-img]: /assets/images/posts/optimalpack-food.png
[meals-img]: /assets/images/posts/optimalpack-meals.png
[old-img]: /assets/images/posts/optimalpack-old.png
