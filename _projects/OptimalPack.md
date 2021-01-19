---
layout: project
title: OptimalPack
git: https://github.com/asgray/HikePlanner
thumb: /assets/images/projects/hikeplanner_thumb.png
tools: [Python, React.js, MySQL, Flask]
---

This application allows backpackers to plan trips and optimize their choice of gear and supplies.

<!--more-->

Backpackers need to carry enough gear food and water to be safe and comfortable, but gear needs to be lightweight and the food easy to prepare and nutrient-dense. It might also all have to fit into a bear can, depending on local regulations. Additionally, its only considered safe for an individual to carry 20% to 30% of their body weight on their back. The result is an optimization problem where a backpacker attempts to carry as much high-value food as they can, and thereby stay in the wilderness for as long as possible without sacrificing necessary gear. The purpose of the OptimalPack application is to provide a calculator that contains information about an individual, specific pieces of gear, certain types of food and different locations. It can be used to generate packing lists, along with statistics like total weight and calorie content of a meal plan. Additional requirements can be displayed to the user, such as regulations that affect choices of food or gear.

The database was implemented with MySQL, and was accessed by a simple, menu-based Python shell script. After the initial project was completed, it was rebuilt using Flask and SQLAlchemy as a backend and React.js for the user interface. The project is currently on hold while I work on Devroast, and will likely be rebuilt again using Django and React when I have learned more.

Download the original design document **[Here](https://github.com/asgray/OptimalPack/raw/master/DBProject.pdf)**
