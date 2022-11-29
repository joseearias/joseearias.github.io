---
layout: post
title:  "Week 9: Deadline"
date:   2022-11-28 18:39:15 -0500
categories: weekly update
---

This whole month was full of headaches and voila! moments, but finally today was the final day to deliver our application, so just as this project started, it ends, and with its end new ones are just on the way. So no time to relax, but at least I can say that I’ve made it past my first project while working as a developer. 

As I have mentioned previously, this application consisted of making the front and back end of a fully working “todo” list application. By the end of this week I realized that I made a mistake by starting completely with the front end of the application. I’m sure a lot of people will not agree with this, but getting your back end to play nice with a fully developed front end can become a real headache.

At the end I got a fully working application that serves its purpose and has most of the functionalities that we were asked to implement. There are some things that I didn’t have the time to work on, like the testing (which is really important when developing an application, by the way) or getting the exception handling to work for each and every possible case.

By the end of this week I realized that I made a mistake by starting completely with the front end of the application. I’m sure a lot of people will not agree with this, but getting your back end to play nice with a fully developed front end can become a real headache.

I took some liberties while connecting both parts of the application. For one I decided that making a request to the back end each time the user needed to filter or search a task was a waste of resources. This is not that obvious when dealing with just one client making calls to the server, but what happens when there are thousands or even millions of users trying to make HTTP requests each time there is a change on the page. For this reason I considered that leaving the front end to deal with these operations was the best solution for this problem. 

So even though most of the functionalities that were asked for the API were done, I left most of the workload to the front end. Some of the cases where I wouldn’t apply this solution would be when dealing with large amounts of data to be saved on the client. But in this case because we are working with just a list of user tasks there is not much of a problem. That being said, I still need to practice and learn how to better implement these functionalities on the back end and how to connect it to the front end.

One of the things I want to do next, other than our assignments to come, is to delve deeper into Spring Boot and see how much you can make without limitations. I started this whole project dreading working with Java, and by the end of it I think I can finally say I took an appreciation for it and its capabilities. I don’t know why but at first I thought working with Spring Boot would be like trying to solve an ancient and complex puzzle, but that isn't anywhere near the truth. Although I honestly still prefer working with Django or Express, I can see why so many developers choose to work with Spring Boot. 

The thing I regret the most for this project was not following test-driven development from the start, because by the time I decided to start working on the tests for my application it was already too late. What I was testing manually every time I made a change on both the front and back end I could’ve made it almost automatically and a lot of time would’ve been saved.
I usually use this approach when coding with other frameworks, but this time I decided that maybe I could’ve postponed it while I learned the fundamentals of Spring Boot.

If I had to start working on the application from the beginning what I would do would be this:

1. Don’t get stuck too much on tutorials if you’re learning a new tool, watch or read a couple of guides and just start working on your project.
2. If working on the full stack of an application, start by having at least an idea of how the communication between both parts will be. 
3. Like I mentioned, I would start by working on the back end of the application, because after doing so you already have data to communicate when starting the front end.
4. Start making your tests as soon as possible. You can even code your tests before starting to code your application. This will save you a lot of time on the run.
5. Once you have a substantial part of the back end you can start by implementing the most basic functionalities on the front end. Just so that you can make changes accordingly to the back end.
6. Keep doing what you’re doing until you have the final product.

I hope that in my next web development projects I can follow these steps so that I can make my life much easier. 

I know that I’m not done working with Spring Boot, because of the following assignments. But to be honest I don’t really mind this. I feel that I’ve learned a lot these past weeks by trying to make my back end from scratch. Not only did I have the chance to get a refresher on many programming concepts, but I had the chance to appreciate what many people do to facilitate our work as developers, like by abstracting huge amounts of code into ready to use libraries or by creating out of the box tools that implement many of the solutions to our problems when writing code.
