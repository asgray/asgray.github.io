---
layout: project
title: DevRoast
git: https://github.com/devroastproject/devroastproject
thumb: /assets/images/projects/code_quality_2.png
tools: [Python, Javascript, Docker, React.js, PostgreSQL, Django, Cypress]
---

An application that allows new software developers to post their projects for feedback.

<!--more-->

_[Cartoon from XKCD](https://xkcd.com/1695/)_

The Devroast app is currently under construction by a few junior developers from the Puget Sound Programming Python _([PuPPy](https://www.pspython.com/app/))_ group. A senior developer has kindly provided guidance, advice, and code reviews. The app uses Docker-Compose to manage a backend api built with Django, a user interface built with React, and a database using PostgreSQL.

So far we have completed the docker-compose setup with a persistent database mount and static asset collection. The app itself extends the stock Django User model and the frontend is set up to allow users to register and log in. The CRUD operations for the Project models are supplied by the Django Rest Framework, and are under construction on the front end.

![ERD](\assets\images\projects\dev-roast-erd.jpg)

Most of the ERD shows the stock Django User tables. The elements in the blue box have been added to support projects, comments, and a tagging scheme, and could be expanded in the future.

![ERD](\assets\images\projects\devroast_landing.png)
![ERD](\assets\images\projects\devroast_detail.png)

Preliminary wireframes of the main page and project detail, respectively.
