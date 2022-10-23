---
layout: post
title:  "1st Technical Log"
date:   2022-10-17 19:09:15 -0500
categories: jekyll update
---

Here I provide a proposed solution to the problem “Double or One Thing”, a problem that was part of the 2022 edition of Code Jam, a competition made by Google to prove yourself and your problem solving skills. 

The details about this problem can be found [here][codejam] and the code for my solution [here][solution]. If you have any question regarding my solution, please reach out to me.
 
<h2>CONTEXT</h2>

Let’s say we had a string that represents a word, for example, the string ‘HELLO’. We can highlight any combination of characters in that string to duplicate said characters and obtain something a new string, like this:
 
H ***E*** L ***L*** ***O*** → HEELLLOO
 
Given a string there are multiple strings that we can obtain doing this, for example the string ‘CAR’ has the next possible set of strings: ‘CCAR’, ‘CCAAR’, ‘CCAARR’, ‘CAAR’, ‘CAARR’ and ‘CARR’.
 
We are trying to find the string that appears first in alphabetical order. For our ‘CAR’ example the first string in alphabetical order would be ‘CAAR’. A string s appears before another string t if s is a prefix of t or if at the first place s and t differ, the letter in s is earlier in the alphabet than the letter in t. For example, the strings ‘ALEX’, ‘ANDREW’, ‘JOHN’, ‘JOSH’ and ‘SANDY’ are in alphabetical order.
 
The inputs to our problems are:
 
T\: integer representing the number of test cases to solve.

S\: strings representing each word that we are trying to solve.
 
For example, for the next input:

```
3
PEEL
AAAAAAAAAA
CODEJAMDAY
```
 
we would have the next output

```
Case #1: PEEEEL
Case #2: AAAAAAAAAA
Case #3: CCODDEEJAAMDAAY
```
 
## SOLUTION
 
Finding the optimal solution to this problem required some experimentation with different strings. There’s no point in calculating each possible obtainable string, because we can know since the beginning that there are some strings that can’t be the first string in alphabetical order. For example, let’s say that we had the string ‘SEEN’’. There’s no way that if a character in position *i* is larger in order than the character at position *i + 1*, the string obtained by duplicating the character at *i* would be smaller than the one that would be obtained by just ignoring it. ‘SSEEN’ is larger in order than ‘SEEN’, ‘SEEEN’ or other cases where ‘S’ isn’t duplicated. So this can be applied to each character on the string. 
 
We can see that if there are strings where the same two or more characters are next to each other, the string obtained by duplicating both characters would be smaller than the one where we don’t duplicate both characters. ‘SEEEEN’ is smaller in order than ‘SEEN’, because at index 3 we would have that the character for the first string would be ‘E’ and for the second string would be ‘N’.
 
The difference with this case would be when the next character that isn’t repeated is smaller in order than the repeated character. For example, with the string ‘LOOK’, the obtained string ‘LOOK’ is smaller than the strings ‘LOOOK’ or ‘LOOOOK’. So we can say that if after a repetition of characters there’s a smaller character than the previous ones then we don’t have to duplicate any of the repeated characters.
 
We can see that we can just iterate through each character on the string *S* and apply these rules to find the best option possible, instead of finding each and every possible combination of strings. This requires just a *for* loop of size of S repetitions. That means a time complexity to solve an *S* string would be ***O(\|S\|)*** with *\|S\|* being the number of characters in *S*.
 
Here is the code for the implementation of my solution.

```python
def test():
    word = input()
    
    result = []
    count = 1

    for i in range(len(word)):
        # checks if it's not the last character on  the string
        if i + 1 != len(word):
            # adds 1 to count if the current character is the
            # same as the next one
            if word[i] == word[i + 1]:
                count += 1
            # appends to the result the current character times 
            # the value in the count variable
            else:
                if word[i] < word[i + 1]:
                    result.append(word[i] * count)
                count = 1

        # appends current character to our result list
        result.append(word[i])
    return "".join(result)


if __name__ == '__main__':
    result = []

    cases = int(input())

    # asks the user for a number of cases and appends the
    # return of each test to our result list
    for case in range(cases):
        result.append(test())

    # prints the result of each case
    for case in range(cases):
        print(f'Case #{case + 1}: {result[case]}')
```
 
If our character at position *i* on S is bigger in order than the one at position *i + 1* there’s no point in duplicating said character. So we just add the character to the result array. 
 
If the character at index *i* is the same as the next character then we can add *1* to our variable count. And this repeats itself until `S[i + 1]` is different from `S[i]`. There’s two possible cases then: The first one is that `S[i]` is smaller in order than `S[i + 1]`, in that case we add the character at index *i* times the value on the variable `count` to our `result` array. This accounts for the number of repetitions found of that character at *S*. The second case is that `S[i]` is bigger in order than `S[i + 1]`. In that case we have to drop adding the repeated characters to the array and move on to the next character.
 
We can see that there’s no point in checking the last character because if we add this character to the string then the obtained string would have a bigger order than the one without this duplicated character.
 
## ALTERNATIVE SOLUTIONS

For my first solution I considered just using Python functionality of `min()` to detect the first string in alphabeticar order of a list containing each and every possible string obtainable. But it is intuitive to notice this approach of calculating and saving each possible string wouldn’t be very efficient, as if we have a string of size *S* the possible number of strings obtainable would be *2<sup>\|S\|</sup>*.

[codejam]: https://codingcompetitions.withgoogle.com/codejam/round/0000000000877ba5/0000000000aa8e9c#problem
[solution]: https://github.com/joseearias/codejam2022/blob/main/round1A/doubleoronething.py
