---
layout: post
title:  "First Entry"
date:   2022-10-17 18:39:15 -0500
categories: jekyll update
---
Hi, there! My name is José Arias. This is the first entry from what I hope are many to come in the next couple of months where I document everything that I’ve learned during the week as a part of Encora’s Apprentice Program. This is the first time doing something like this so excuse my writing abilities if I’m not that good at this writing stuff yet.

For my first entries I’ll be using Jekyll and Github Pages for the blog, but I’m hoping that within the next few weeks I’ll be able to move all my entries and the ones to come to its own ground up built application.

This week the rest of the Apprentices and I were assigned some algorithmic problems that we needed to solve as a team in 4 different programming languages, these being Python, Dart, Kotlin and Typescript. These problems are part of the problems used in Google’s Code Jam coding competition for the 2022 edition. 

The first lesson of the week was how to efficiently work as a team. Organizing the schedule and trying to solve the problems together was a really valuable experience. As a team we decided that the best course of action was to solve the logic involved with each problem together and then individually try to translate the proposed solution into one of the programming languages of our choice. I decided to use Typescript for mine, because although I’m used to code in Javascript I’ve never taken the time to use or learn TS before, so I thought this would be a good time to get familiar with it.

The problem that I chose was `3D Printing`. You can find the problem [here][code-jam] and my solution in Typescript [here][ts-solution].

Starting to learn a new programming language is always fun. Of course, that’s not to say there’s always little things you have to get the hang of before you can actually start using said programming language to actually make stuff. This week I had the task of learning the basics of Typescript, which I didn’t have much problems doing because of it being a superset of Javascript. But because of Typescript being basically Javascript with static typing, it has some of the same issues that you had to deal with when using JS. 

Because of the nature of the tests that Google uses for Code Jam, the input that each program needs and how you get that input follows a specific format depending on the programming language used for a problem. When using a programming language like Python this is not a problem. Using the function `input()` and applying some operations on the data received is enough to get the input that you need, and usually when coding in Javascript the most common used method for getting input from the user is by using the function `prompt()` which displays a dialog box that prompts the user for input. but when dealing with console input that is another case completely. And I think solving this was the biggest headache during the week, but nothing too bad.

For this case it is necessary to build an interface that reads each line of input from the console, with the help  of a Node.js module called `realine` that provides this interface. This module helps us read data from a stream one line at a time. After that you need to extract the data needed for each line, which results in its own algorithmic problem although not as complicated as the real coding problem that was being solved. Once that is done, you have to manually interrupt the program to stop the running execution context to make run the callback function in charge of solving the cases of the problem. So not as intuitive as one might think. After dealing with this situation it was time to tackle the algorithmic problem which wasn't very difficult after having discussed it with the team. And writing this part of the code wasn't an issue after having used getting the hang of the differences between TS and JS.

Other than this problem I had time to solve the individual problem that we were assigned too. This problem it's also part of the problems given during the 2022 edition of Code Jam. We were given the option of choosing between 3 problems and I decided to go for `Double or One Thing`, which was a problem about strings that required a little bit of dusting off of my Algorithms classes of University. I used Python for this just to have it finished as soon as possible. But I hope this next week I can tackle the problem in Typescript as well, just to keep learning its ins and outs. You can find the problem [here][code-jam2] and my solution for it [here][py-solution].

By the end of the week I realized how much the assignments and readings we were given previous weeks helped me to dive into these week problems. Learning to organize my time better, how to stick to good habits, how to deal better with stress and my own insecurities, and how to approach learning has been really valuable during this first week of technical assignments. And I hope that during the next couple of weeks I can put more of that into practice and get better at it.

I can say that this week was a really fruitful one, and without a doubt my favorite part of it was having the time to learn more about my teammates and how to work efficiently with them. The help and support that we give each other is really valuable and I hope this makes us all not only better programmers but also better persons by the end of this experience.


[code-jam]: https://codingcompetitions.withgoogle.com/codejam/round/0000000000876ff1/0000000000a4672b

[ts-solution]: https://github.com/joseearias/codejam2022/blob/main/qualification/punchedcards.ts

[code-jam2]: https://codingcompetitions.withgoogle.com/codejam/round/0000000000877ba5/0000000000aa8e9c#problem

https://github.com/joseearias/codejam2022/blob/main/round1A/doubleoronething.py