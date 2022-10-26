---
layout: post
title:  "Team Work"
date:   2022-10-23 15:36:15 -0500
categories: jekyll update
---
Working efficiently as a team is not always a piece of cake. But when there's enough commitment from all members, things can get done even against the odds. 

During the last two weeks, the rest of the Apprentice Team at Encora and I had to solve 8 different exercises from the 2022 edition of Code Jam in 4 different programming languages, these being Python, Kotlin, Dart and Typescript, so in total there were 32 different programs made by our team. We can say that even though there were a lot of obstacles and head scratching moments, we learned a lot of things about working as a team, and of course, we learned how frustrating it can be to make your code work in a new programming language but at the same time how regarding it ends up being. 

This is a technical log of the approach that we as a team had for the exercises and at the same time I write a little bit about my contribution to this assignment.

# PROBLEM 1. Punched Cards

## OVERVIEW 

Punched Cards is a problem that deals with array manipulation, where given the integers R = Rows and C = Columns describing the size of a punched card, you need to print the ASCII art drawing of it as described. 

Here is an example with R=3 and C = 4: 

```
. . + - + - + - + 
. . | . | . | . | 
+ - + - + - + - + 
| . | . | . | . | 
+ - + - + - + - + 
| . | . | . | . | 
+ - + - + - + - + 
```

## CONTEXT  

What is Punched Cards about? 

A secret team of programmers is plotting to disrupt the programming language landscape and bring punched cards back by introducing a new language called Punched Card Python that lets people code in Python using punched cards! Like good disrupters, they are going to launch a viral campaign to promote their new language before even having the design for a prototype. For the campaign, they want to draw punched cards of different sizes in ASCII art. 

The ASCII art of a punched card they want to draw is similar to an R×C matrix without the top-left cell. That means, it has [(R⋅C) − 1] cells in total. Each cell is drawn in ASCII art as a period (.) surrounded by dashes (-) above and below, pipes (\|) to the left and right, and plus signs (+) for each corner. Adjacent cells share the common characters in the border. Periods (.) are used to align the cells in the top row. 

## SOLUTION

There's not much to say about the solution of this problem. We can divide the problem in two parts, one that prints the part of the punched card without the top-left cell, and the other part prints the rest of the card. 

For the first part we just need to create a loop that creates the string lines that represent the borders of each row and columns. These strings are built concatenating the characters '+' and '-' for one case, and '\|' and '.' for the other one. And after that we just print one of each with the string '..' added to the start of each line. After printing the first part of the card we move on to create the rest of the punched card.

For the second part we have to make 2 diferent loops to create again the lines that define the borders of the rows and columns of the card. Each row and column is built again by the strings '+-' and '\|.'. The only detail is that we need to concatenate the last member of each string separately. Once we have saved these strings into variables we can print them with two different loops that draw the rest of the card. At the end we just need to print manually one more string to give the bottom border of the card.

Here is my code for the implementation of the solution in Typescript.

```typescript
declare var require: any;
declare var process: any;

const readline = require('readline');
let rl = readline.createInterface(process.stdin, process.stdout);

// Defines an interface for the data needed for each test case
interface TestData {
    testNumber: number;
    rows: number;
    cols: number;
}

// Parses each line of input and split into the data needed for each case
function parseInput(input: string[]) {
    let line: number = 0;
    
    // Reads the number of test cases from the first line of input
    const numCases = Number(input[line++]);

    const testData: TestData[] = [];

    for (let testNumber = 1; testNumber <= numCases; ++testNumber) {
        // The first number of each line contains the number of rows of each case
        // and the second number contains the number of columns.
        const rows = Number(input[line].split(' ')[0]);
        const cols = Number(input[line++].split(' ')[1]);

        testData.push({testNumber, rows, cols});
    }
    return testData;
}

function runTestCase(data: TestData) {
    // Prints the case number into the console
    console.log(`Case #${data.testNumber}:`);

    let card: string = '';
    card = card.concat('..');

    for (let i = 0; i < data.cols - 1; i++) {
        card = card.concat('+-');
    }
    card = card.concat('+\n..');
    for (let i = 0; i < data.cols - 1; i++) {
        card = card.concat("|.");
    }
    card = card.concat('|');

    // Prints the first row into the console
    console.log(card);

    let plus: string = '';
    let bars: string = '';

    // Creates the string for the '+' and '-' symbols
    for (let i = 0; i < data.cols; i++) {
        plus = plus.concat('+-');
    }
    plus = plus.concat('+');

    // Creates the string for the '|' and '.' symbols 
    for (let i = 0; i < data.cols; i++) {
        bars = bars.concat('|.');
    }
    bars = bars.concat('|');

    // Using the strings that we defined earlier we can create the rest
    // of the punch card.
    for(let i = 0; i < data.rows - 1; i++) {
        console.log(plus)
        if (i === data.rows) continue;
        else console.log(bars);
    }
    console.log(plus);
}

function runAllTests(input: string[]) {
    const testCases = parseInput(input);

    testCases.forEach(runTestCase);
}
```

We can clearly see that there are five loops with at most the maximum value between the number of rows and columns operations each. So we have a time complexity of **O(<sup>max(|r| | |s|)</sup>)** being r and s the number of rows and columns of the card respectively.


# PROBLEM 5. Twisty Little Passages

## OVERVIEW 

Twisty Little Passages is a problem that deals with probability and importance sampling. You are given the total rooms and the number of operations that you can do for every case. You need to implement a way of asking the user every move you want to do by teleporting and walking a total of K times, getting all the degrees possible and also a good estimation of a degree average, this in case there is still rooms left to visit by our K operations. 

In our solution we implemented the following graph formula for edges (passages in problem): 

Edges (Passages) = ΣDegrees/2 

For this type of problems there is no pure scientific correct way of solving, here you need to implement enough heuristics so that you are fairly certain that you are close to a good estimate. 

## CONTEXT 

What is Twisty Little Passages about? 

You are investigating a cave, which is a simple undirected graph with N vertices and no isolated vertices. At the start you are told that the cave has N <= 10^5 rooms. The vertex number you are at and the number of incident edges.  

When in a room, you can identify what room you are in and see how many passages it connects to, but you cannot distinguish the passages. You want to estimate the number of passages that exist in the cave. You are allowed to do up to K = 8000 operations. An operation is either: 

Teleport: You choose to teleport to a vertex number of your choice 

Walk: You choose to be moved to a uniformly chosen random neighbor of the current vertex. 

After each move, you are told the vertex number and the number of incident edges. With this information you have to estimate the number of edges in the graph in an approximation error of 33.3%, and you are to succeed in at least 90% of the test cases. 

# PROBLEM 6. Double or One Thing


