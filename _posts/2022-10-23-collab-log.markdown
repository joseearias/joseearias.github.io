---
layout: post
title:  "Collab Log"
date:   2022-10-23 19:39:15 -0500
categories: jekyll update
---
Learning how to work as a team is not a piece of cake.

OVERVIEW 

Twisty Little Passages is a problem that deals with probability and importance sampling. You are given the total rooms and the number of operations that you can do for every case. You need to implement a way of asking the user every move you want to do by teleporting and walking a total of K times, getting all the degrees possible and also a good estimation of a degree average, this in case there is still rooms left to visit by our K operations. 

In our solution we implemented the following graph formula for edges (passages in problem): 

Edges (Passages) = ΣDegrees/2 

For this type of problems there is no pure scientific correct way of solving, here you need to implement enough heuristics so that you are fairly certain that you are close to a good estimate. 

------------ 

The first approach was to just teleport and visit 8000 random chosen vertices, using all of them to estimate the average degree of all the vertices, this kind of works, but if the graph is in a star shape where all of the passages connect to a center, there is a high chance you don’t hit the center by teleporting, causing the sample to average every degree to 1. 
One way to fix this is to teleport once, then walk once, so in case of a star your chances of hitting the center is 100%, and not just a tiny fraction. Like this: 
Repeat 4000 times: 

Randomly teleport to an unexplored vertex  

Walk 1 time to a random neighbor 

In order to be able to teleport to an unexplored vertex, to maximize chances of seeing something new we need to use a set, which will let us store unseen places and to ignore the ones we already visited thanks to its property of hashing. This will also result in an optimized solution since the look up and insertion time complexity of the set is of O(1) 

CONTEXT 

What is Twisty Little Passages about? 

You are investigating a cave, which is a simple undirected graph with N vertices and no isolated vertices. At the start you are told that the cave has N <= 10^5 rooms. The vertex number you are at and the number of incident edges.  

When in a room, you can identify what room you are in and see how many passages it connects to, but you cannot distinguish the passages. You want to estimate the number of passages that exist in the cave. You are allowed to do up to K = 8000 operations. An operation is either: 

Teleport: You choose to teleport to a vertex number of your choice 

Walk: You choose to be moved to a uniformly chosen random neighbor of the current vertex. 

After each move, you are told the vertex number and the number of incident edges. With this information you have to estimate the number of edges in the graph in an approximation error of 33.3%, and you are to succeed in at least 90% of the test cases. 
