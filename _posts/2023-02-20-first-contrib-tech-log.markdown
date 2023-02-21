---
layout: post
title:  "Technical Log: Open Source First Collaboration"
date:   2023-02-20 12:39:15 -0500
categories: technical-log
---

This is the technical log for my first open source contribution. As my first contribution I chose to tackle an issue inside the web.dev repository. Web.dev is a learning resource made by Google to teach fundamental web development concepts. Because I’ve used this resource in the past I decided that it would be a good idea to help in some way as well.

The issue to be solved were a couple of broken links that showed a 404 error page on screen when visited. 

Issue: (https://github.com/GoogleChrome/web.dev/issues/9244)
Pull Request: (https://github.com/GoogleChrome/web.dev/pull/9614)

Date: 2023-02-19

## Steps Taken:

Issue Analysis - I started by analyzing the issue reported in the repository. The problem seemed to be two links that were not functioning correctly inside the Identity section of web.dev. The links were showing a 404 error page. So the first step was checking where those links were written on the actual code.

*Code Review* - I went through the codebase to see where the issue could potentially be, and found that there was a problem with how the routes were implemented with i18n. In the json file detailing the routes for the identity section were the URL for link. There seemed to be a problem with how the nested routes were interpreting the absolute path.

*Code Changes* - I implemented the proposed solution by making the necessary code changes to the identity.js file. This was made by putting the correct absolute URLs into the broken links. I tested the changes locally to make sure they were working as expected.

*Pull Request Creation* - A pull request was created on GitHub with the code changes that I made. I included a detailed description of the changes made.

*Code Review by Peers* - The pull request was then reviewed by other contributors to the repository. They analyzed the code changes and approved the code.

*Tests and CI/CD* - Once the code was approved by the repository maintainers, a test flow was done to check that the code could be merged safely with the rest of the main branch. 

*Pull Request Approval and Merge* - After passing all tests, the pull request was approved and merged into the main branch of the repository.

*Issue Closing* - Finally, one of the code maintainers closed the issue that was reported and linked the pull request that solved the issue to it, so that future users can track the solution.

## Summary:

In summary, I analyzed and solved an issue with some malfunctioning links on the GoogleChrome/web.dev repository. I found a solution to get rid of this problem while looking inside the codebase, made the necessary code changes, went through code review, and merged the pull request after passing all tests.

Even though this was my first contribution to an open source project, I learned a lot of things about how big projects approve and implement the code and other kinds of contributions with their project.
