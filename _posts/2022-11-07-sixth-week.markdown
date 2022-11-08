---
layout: post
title:  "Week 6"
date:   2022-10-17 18:39:15 -0500
categories: weekly-update
---

I’ve been working for the last week on my To Do list application. Like I mentioned in my previous post, this app consists of both a front end that works as the UI and a Rest API to receive and upload data. The front end is done with React.js and the API that works as the back end is done using Spring Boot.

## The state of things by now and why I love Vite

Most of the front end of my application is done by now. Is only a matter of making sure it gets along well with the Rest API. For a faster and more stylish development of the front end I used Material UI which is a React component library that offers a vast collection of pre-built components which save you time on the style aspect of the application and lets you concentrate on the logic behind the communication with the back end.

The other thing worth mentioning is that this week I discovered the greatness of Vite as an alternative build tool for React projects. And I cannot be more happy about it.

Before this project I’ve exclusively used only the Create React App tool for my React applications, and I should've known what a difference using Vite would make in my development experience. 

As your React project grows in size Create React App’s performance really gets a hit, and the time it takes to build your application grows at a fast rate. This is not the case so much with Vite, where at any moment I stood up waiting for my code to build and run on the browser for more than a second. 

The main reason for this difference in development times is that CRA makes use of Webpack and its approach to handling the compilation is that every time something changes in the code it bundles all the source code and dependencies it needs to. The result is that as the project grows larger, the building process becomes slower as well. Vite doesn’t bundle the entire application every time there is a change, this is done only one time the first time the development server is started and transpiling is done when it is needed to. This makes Vite faster than CRA.

Overall I find working with Vite more enjoyable and it gives me a cleaner project structure which is nice. For the moment I’ve made the switch to Vite for my React and other Javascript related projects.

## Getting things done in the back

Usually a todo application it’s the first thing I build when learning a new framework, because it gives you the chance to implement all of the basic CRUD operations into it, and coding it gives you a fair understandment of most of the functionalities said framework offers. So in this case building a todo app to start learning Spring Boot was a helpful experience.

For the moment I’ve only implemented the basic GET and DELETE methods to the application. But by the end of this week I’m hoping that all the CRUD operations will be implemented and working, it will only be a matter of creating the tests and making the correct validations for the data that it’s received on the server.
For a long time I dreaded working with Java for any project because at first sight it seems strange and cumbersome, but the more I use it the more comfortable I get with it. And breaking things and making them work again has helped me to familiarize so much more with this programming language. I’m thinking of working on more coding projects with Java and Spring Boot in the future so that I can make my own mind of the benefits of using these technologies for my own projects. 

So, for this next week I’m planning to dive a little more into Spring and Spring Boot and work on the final functionalities of my application. Fingers crossed I finished most of the project by the end of the week and I can concentrate on the final details next week.

