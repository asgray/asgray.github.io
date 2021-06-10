---
layout: post
title: "Adventures In Front-End Testing"
date: 2021-06-09 21:00:00 -0700
categories: programming
tags: [React.js, Cypress]
thumb: /assets/images/posts/devroast-testgoat.jpg
project: DevRoast
---

The Devroast UI has grown in complexity to the point that manually clicking things is no longer an efficient way of testing new features. Automating those clicks was a journey.<!--more-->

My first attempt was with Selenium, chosen mostly because it was a name that I recognized. I found an example of integrating Selenium with Django, but ran into problems getting it to work within the Docker Compose. The setup used a hub container to coordinate tests with a cluster of other, browser-specific containers, and I quickly got bogged down trying to coordinate environment variables between multiple containers. Even though I was using the Python version of Selenium, the configuration was in Java. I haven’t touched Java in years, the project is already a mix of Python and Javascript, and I didn’t want to add a third language if I could avoid it. One major advantage to this setup is that it used Django’s built-in test suite to send out the Selenium tests. It would have been able to run all tests, front-end and back-end, from a single console command, but that later convenience involved a lot of early headache. I switched plans.

![goat-img]

The second scheme I looked into was using Jest to write unit tests. Jest is a Javascript testing framework, and is included when a React project is initiated from the command line. However, I quickly realized that Jest wasn’t the tool I needed. At that point, I was still trying to write end-to-end tests, or tests that automated the complete application. Jest offered unit tests for my React components, but none of the components in Devroast are especially complex. With very few exceptions, all the components either query the API or render the results of those queries in HTML. They’re simple enough that debugging their behavior is as simple as glancing at the source code, and I was more interested in testing the behavior of the application as a whole. I also spent some time trying to decide how to handle the database during tests. Ideally, I’d be able to persuade Django to start up a test database, run the front-end tests against it, and drop it when the tests were done. From what I understand, Django can do this, and even does it automatically if the tests are being run with its own testing function. However I again ran into the challenge of coordinating two separate systems across multiple Docker containers and all of the extra complexity that comes with it.

I eventually settled on using Cypress to write and run the front-end tests. Cypress is a framework that allows one to control the testing environment as completely or as little as needed. It also comes with it’s own UI that shows the tests running step by step in the browser. These steps are saved and can be rewound for debugging purposes, and it even has options for saving videos of the testing run, as well as screenshots of test failures. It also automatically handles asynchronous waiting, state cleanup, and API interception and is very user friendly in general. There is a bit of a learning curve, since every Cypress command is asynchronous, and it took me writing a few bad tests before I completely absorbed the logic of how to chain commands together. In the end though, the tests came together quickly once I found a workable framework.

![cypress-img]

<p style="text-align: center;"> Cypress UI in action. </p>

The one minor reservation with this setup is that I never got true end-to-end testing to work. I was trained as a scientist, and the fact that the API calls don’t actually reach the API is an uncontrolled variable that makes me a little itchy. Yes, the front end can mock API responses, and yes, the back end can mock API requests, but the quality of that mocking is only as good as the tests I wrote and cannot itself be tested directly. I would have rather had full end-to-end testing, but the framework I wound up with should be more than enough to scaffold new features and prevent breaking changes. If this post has a moral, it is all about finding the point of diminishing returns and stopping work when the benefits of a feature are outweighed by the effort it costs.

All in all though, I’m glad to have set up testing for the app. I’m looking forward to building out more features, and the Cypress testing system should make doing so faster and easier.

[goat-img]: /assets/images/posts/devroast-testgoat.jpg
[cypress-img]: /assets/images/posts/devroast-cypress.png
