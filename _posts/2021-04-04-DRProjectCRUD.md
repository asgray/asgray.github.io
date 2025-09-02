---
layout: post
title: "Frontend CRUD Operations"
date: 2021-04-04 16:38:00 -0700
categories: programming
tags: [React.js, Django]
thumb: /assets/images/posts/devroast-FrontEndERD.png
project: DevRoast
---

Basic CRUD operations have been added to DevRoast using React.<!--more-->
Specifically, CRUD (Create, Retrieve, Update, Destroy) operations for the Project entity have been added to the front-end of the DevRoast project. The backend routes were provided by the Django Rest Framework boilerplate models, but several don't work without the proper user token.
Previously, the front-end only allowed a user to log in and to change their password. A component called ProjectList was added to retrieve all projects and render them in a list on the main page. For now this component simply uses `map()` to render the list of ProjectPreview components. At some point pagination and sorting will need to be added, probably with React Table. Clicking on a project routes to a ProjectPage component showing the details for that project using the `useParams()` hook and the Switch component from React Router.

If the logged in user is the same as the author of the project, buttons for editing or deleting the project are also rendered. The Delete button triggers a DELETE request directly from ProjectPage (after a browser confirmation), and the Edit button swaps out ProjectDetail for ProjectForm and populates the form with the project information. ProjectForm can also be accessed from the navbar. If accessed from the navbar, it triggers a POST request, but if accessed from the ProjetPage it triggers a PUT request.

A lot of the work on this feature went into polishing the expected behavior of the app after an API call. I used the `useHistory()` hook to forward to the home page or refresh the current component depending on the API call and it's return code. Additionally, I needed to add a conditional rendering of the Login component to many routes in case they were called without authorization. Previously, each component handled checking for a logged in user differently, but it is more concise and easier to manage if the check happens in the Switch in the same ways.

Lastly, I added persistent login using local storage. The app stores the token as well as a timestamp, and whenever an API call succeeds it updates that timestamp. Whenever the app loads, it checks for the token and if it is less than half an hour old, uses it to log the user in automatically. If the time stamp is too old, the Login component is rendered.

![erd-img]

The diagram above shows the relationship between each comonent in the front-end app. I've used standard Chen notation in the places where one component renders another, and arrows where components link to others. Essentially, the App always renders the NavBar and one other based on the Switch. Each other component is rendered based on the links in the Switch and navigated with anchor tags and `useHistory()`.

The diagram won't be extended much further at this point, since the only other two entities are comments and tags, and both will mostly be displayed by the ProjectPage component. Some details might shift, but the app as a whole is relatively simple. After getting all the components up and running, the rest of the project will mostly be adding visual and functional polish.

![demo-img]

It can certainly use some polish. Trust me, it works much better than it looks.

![git-img]

One last note is that I have been getting a lot of practice with Git. I needed to do a lot of squashing, merging and cherrypicking after I mixed up a few commits on different branches. GitKraken has been an extremely helpful tool for visualizing the graph, and for untangling my mistakes. It looks much nicer now.

[erd-img]: /assets/images/posts/devroast-FrontEndERD.png
[demo-img]: /assets/images/posts/devroast-frontend.png
[git-img]: /assets/images/posts/devroast-gitkraken.png
