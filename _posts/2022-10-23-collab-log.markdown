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

We can clearly see that there are five loops with at most the maximum value between the number of rows and columns operations each. So we have a time complexity of **O(max(|r| | |s|))** being r and s the number of rows and columns of the card respectively.


# PROBLEM 5. Twisty Little Passages

## OVERVIEW 

Twisty Little Passages is a problem that deals with probability and importance sampling. You are given the total rooms and the number of operations that you can do for every case. You need to implement a way of asking the user every move you want to do by teleporting and walking a total of K times, getting all the degrees possible and also a good estimation of a degree average, this in case there is still rooms left to visit by our K operations. 

In our solution we implemented the following graph formula for edges (passages in problem): 

Edges (Passages) = Σ(Degrees/2)

For this type of problems there is no pure scientific correct way of solving, here you need to implement enough heuristics so that you are fairly certain that you are close to a good estimate. 

## CONTEXT 

What is Twisty Little Passages about? 

You are investigating a cave, which is a simple undirected graph with N vertices and no isolated vertices. At the start you are told that the cave has N <= 10^5 rooms. The vertex number you are at and the number of incident edges.  

When in a room, you can identify what room you are in and see how many passages it connects to, but you cannot distinguish the passages. You want to estimate the number of passages that exist in the cave. You are allowed to do up to K = 8000 operations. An operation is either: 

Teleport: You choose to teleport to a vertex number of your choice 

Walk: You choose to be moved to a uniformly chosen random neighbor of the current vertex. 

After each move, you are told the vertex number and the number of incident edges. With this information you have to estimate the number of edges in the graph in an approximation error of 33.3%, and you are to succeed in at least 90% of the test cases. 

## SOLUTION

For this problem some of us needed to dust off some of our discrete mathematics classes knowledge. The problem is basically a graph theory problem with a little bit of probability added to it. We need to see the rooms in the cave as nodes in a graph and each passage from a room as an edge from a node. So it's clear to see that this problem could be solved easily if we had a way to know how many passages each room has as we would only need to sum all passages from all rooms and divide the result by 2. But because we only have K operations allowed to check the number of passages from each room, we need to find the optimal way to make use of our permitted operations, these being the ones mentioned in the context of the problem. 

To solve this dilemma, we can divide the number of times we make each operation into a 50/50, as if the number of teleportation grows, the probability of not traveling to each room grows as well. But at the same time it would be a problem if we only walked into each room, as we would necessarily have to walk into rooms already visited. Having the same number of operations per permitted operation makes it less possible to visit a room we already have. So for K operations, K/2 the times we walk into a room and K/2 are the times we teleport into a "random" room.

Now we can have a counter of the passages for each new room we visit that we haven't been in, and have an inventory of the rooms we haven't visited yet. We can add all the passages from each new visited room to the counter and take that room off from our inventory. Once all operations have been done we can just add the sum from our counter to the average of passages we have seen on the visited rooms times the number of elements left in our inventory, and the result from that operation divided by two to get the estimated number of passages from the cave.

Here is the implementation for the solution on Typescript.

```typescript

declare var process: any;
declare var require: any;

// using module 'readline'
const readline = require('readline');
// creates an interface to receive input and print output
let rl = readline.createInterface({
    input: process.stdin, 
    output: process.stdout,
    terminal: false
});

// function to parse strings into two different variables
const parseInteger = (input: string) => {
    let [a, b] = input.split(' ').map((str) => Number(str))
    return [a, b]
}

var candidates = new Set();

let T: number;                  // number of cases
let counter: number = 0;        // counts the number of cases solved
let case_counter: number = 0;   // counter used in each individual case
let part: string = "first";     // used to divide each case in two different parts

let [N, K]: [number, number] = [0, 0];
let [R, P]: [number, number] = [0, 0];

let degree = 0;
let degree_T = 0;
let count_T = 1;

rl.question('', (cases) => {
    // Assigns T cases through line of input
    T = Number(cases)

    rl.on('line', (input) => {
        // Parses number of rooms and number of operations
        if (part === "first") {
            [N, K] = parseInteger(input)
            // makes set of N elements from 1 to N
            candidates = new Set()
            for (let i = 1; i <= N; i++) {
                candidates.add(i)
            }
            part = "second";

        // Parses current room and observable passages
        } else if (part === "second") {
            [R, P] = parseInteger(input)
            
            // if K operations are done then end current case
            if (case_counter === K) {
                if (candidates.has(R)) {
                    candidates.delete(R)
                }
                let degree_avg = degree_T / count_T
                let result = Math.floor((degree + degree_avg * candidates.size) / 2)

                console.log(`E ${result}`)

                part = "first";
                case_counter = 0;
                counter += 1;

            } else {
                // checks if its the first R, P input
                if (case_counter === 0) {
                    if (candidates.has(R)) {
                        candidates.delete(R)
                    }
                    degree = P
                    degree_T = degree

                    console.log('W')
                } else if (case_counter % 2 === 0) {
                    // walk
                    console.log('W');
                } else {
                    // teleport
                    let a = candidates.values().next()
                    console.log(`T ${a.value}`);
                    degree_T += P;
                    count_T += 1;
                }
                // if room is in candidates delete it from set
                if (candidates.has(R)) {
                    candidates.delete(R)
                    degree += P;
                }
                case_counter += 1;
            }
        }
        if (counter === T) {
            rl.close()
        }

    }).on('close', () => {
        process.exit
    })
})
```

# PROBLEM 6. Double or One Thing

The individual log for my solution of this problem can be found on another [post][doot].

[doot]: https://joseearias.github.io/jekyll/update/2022/10/18/first-tech-log.html


