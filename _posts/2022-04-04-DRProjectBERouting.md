---
layout: post
title: "Back-End Routing"
date: 2022-04-03
categories: programming
tags: [React.js, Cypress, Django]
thumb: /assets/images/posts/devroast-monkeywrench.jpg
project: DevRoast
---

So far I've been focusing on building the DevRoast user interface, I had to familiarize myself with the server-side framework in order to add the remaining features.

<!--more-->

The DevRoast app has two main parts: the front-end built with React and the back-end built with Django. While I am generally more comfortable working with Python than I am with Javascript, I hadn't seen Django before the beginning of the project. The basics of the back-end were set up by someone with Django experience, and I was able to take it for granted while setting up the UI. The Django REST Framework comes with CRUD (Create, Retrieve, Update, Destroy) operations for database entities working out of the box, but I needed more complex back-end behavior in order to add the remaining functions to the app.

![monkey-img]

<p style="text-align: center;"> Pictured: The author learning a new framework </p>

My first task was to get Comments to form discussion threads. We already had a pretty good model to handle comments, so all that needed to change was how the objects were nested in an API reply. I knew that the Project serializer needed to collect all related comments with a `null` prompt, and each of those comments would in turn collect all comments related to them by the prompt field. The goal was clear enough, but I needed to spend some time trawling the docs and, eventually, asking for suggestions since it wasn't immediately clear to me how the Serializer classes interacted with each other. Eventually I ended up using `SerializerMethodField()` to trigger nested serialization and allow the React app to collect all the information for a single Project in a single API call.

Successfully organizing Comments into threads also raised the question of how to handle deletions. Deleting a Comment without any replies is straightforward enough since it isn't referenced by any other object. However, I had to decide how to handle the deletion of a comment with one or more replies. Cascading the deletion was an option, but as this app was intended to have similar functions to Stack Overflow, it seemed like there would value in leaving replies visible even when the prompt had been deleted. To achieve this, the `destroy()` method was overwritten. Any Comment with a prompt or that had no replies is deleted as normal, but otherwise it is changed to "This Comment Has Been Deleted," its vote counts are set to 0 and the thread is closed. The comment itself is removed, even if the Comment entity still persists in the database along with any replies. Close enough.

Setting vote counts to 0 didn't last very long. As I began building out the UI for voting on comments, I realized that the user was able to vote multiple times on the same comment. Since the negative and positive votes were an attribute of the Comment, there was no logic to prevent the same user from casting multiple votes, or even a positive and a negative vote on the same Comment. In order to add mutual exclusion to the votes, they were split off into their own Vote model comprising the comment in question, the user casting the vote, and a Boolean value for whether or not it was a positive vote. The unique combination of User and Comment prevents multiple votes, and the Boolean vote ensures mutually exclusive positive and negative votes. This was also an opportunity to learn more about the Django Rest Framework. Creating a new model meant that URLs had to be registered, and even though the views and serializer didn't need anything beyond the DRF boilerplate, they still needed to be set up.

The third and final function I added was the Tag system. A model for Tags already existed, but I wanted to be able to use it to tag both Comments and Projects, so it needed a small adjustment. Essentially, the change was to use `ManyToManyField()` with `blank=True` twice in order to relate a Tag with a Comment and/or a Project or to allow it exist independently. The view also needed an update to `update()` in order for Django to correctly determine if a Tag/Comment or a Tag/Project relationship was changing. Only the `update()` method needed to be touched, since the other CRUD methods haven't been added to the app yet.

So far I've been writing about the back-end changes because those were the largest learning opportunities for me during this phase of the project, but adding these three features also required a fair amount of front-end work. The reply threads and vote system were relatively straightforward since they both nest neatly with other entities, but the Tag system was a different story. I wanted a group of components that could be plugged into Project and Comment components, so some experimentation was necessary. I shifted the component structure around a few times before settling on giving Tags their own independent form and having the main App component query a master list of all existing Tags to use as a single source of truth. Something about that solution feels inefficient to me, but since the list of Tags should never get especially long, and because I don't expect Tags to be changed very often even when the CRUD operations are added, I think it should be fine. Either way, this is the final(ish) front-end ERD as it stands with all main functions implemented:

![erd-img]

<p style="text-align: center;"> The latest DevRoast functional ERD </p>

I also want to quickly mention that running my front-end tests with Cypress has worked out better than expected. Any time I needed to restructure the React components I could be confident that I hadn't broken anything or that I would be informed of exactly what had gone wrong. I also found myself using the testing files as a functionality checklist, adding new test stubs as I imagined potential edge cases or user interactions and using those stubs to guide the actual component development. In addition to all the normal test-driven development stuff, watching the Cypress browser blast through all the different button clicks and come back with a perfect score is just so satisfying.

DevRoast is a fully functional app now! The next step is to add some styling and polish, because the bare HTML could look a lot better.

[monkey-img]: /assets/images/posts/devroast-monkeywrench.jpg
[erd-img]: /assets/images/posts/devroast-FrontEndERD2.jpeg
