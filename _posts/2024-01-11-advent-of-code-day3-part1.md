---
layout: post
title: advent-of-code-day3-part1
date: 2024-01-11 10:00:56 -0800
categories:
---
### Advent Of Code Day 3 Part 1
This one was a lot more difficult that I thought it would be. However, I learned a lot about how python works.

## The problem
You are presented with rows of text that have symbols, numbers, and periods. You job is to find a number that is adjacent to a symbol that isn't a period.
link [adventofcode.com day 3][day3]

## what I did,
1. Saved the file as plain text again, but had to do something a little different.
2. Created two functions to repeat a process I don't want to do by hand.
3. Figured how to avoid a `try` and `finally` functions.
4. A couple `for` loops and a lot of `if` statements.

## How I solved it

When you open a file in python, it read that file 1 line at a time. So, I had to break it up. To do this, I just made a really big `dictionary` with keys as integers and values as the string.
``` python
with open("data.txt", "r") as file:
    score = 0
    table = {
            }
    listSymbols = ["!","@","#","$","%","^","&","*","(",")","-","_","=","+",",","<",">","/","?"]
    listNums = ["1","2","3","4","5","6","7","8","9","0"]
    incr = 0
    temp = [None]
    for i in file:
        table.update({incr:""})
        for j in i:
            if j == "\n":
                break
            table[incr] = table[incr] + j
        incr += 1
```
After that, I did 2 `for` loops to go threw each line and character looking for symbols"---"since they appear the least"---"for efficiency. From there, All I did was if statements to look in all directs for a number.
``` python
for i in table.keys():
    for j in range(len(table[i])):
        symbol = table[i][j] # prevent repeating myself
        strLen = len(table[i])-1 # prevent repeating myself
        if symbol in listSymbols:
            # up
            if i > 0:
                if table[i-1][j] in listNums:
                    appendToList(myFunc(j,table[i-1]))
                # left up
                if j > 0:
                    if table[i-1][j-1] in listNums:
                        appendToList(myFunc(j-1,table[i-1]))
                # up right
                if j < strLen:
                    if table[i-1][j+1] in listNums:
                        appendToList(myFunc(j+1,table[i-1]))
--- break in text ---
```
As you can see above, there are two functions I am using to append to the `list` called temp. `myFunc`, was used to count back in the string to find the first integer in the number and return the result. The second function called `appendToList`, is used to make sure it isn't returning `None`, which is useless to me.
`myFunc`, took in two variables, the index of the string, and the string its self. From there it would count back to find the first integer. The last thing it did was make sure that the number wasn't the same as the last one in the list"---"accidental repeated number.
``` python
def myFunc(index, string):
    part = ""
    if index > 0:
        for x in string[index::-1]:
            if x in listNums:
                index -= 1
            else:
                index += 1
                break
    if index < 0:
        index = 0
    for x in string[index:]:
        if x in listNums:
                part = part + x
        else:
            break
    if part != temp[-1]:
        return part
```
`appendToList`, was simple, make sure that you aren't appending `None`! It was interesting to see that python functions return `None` regardless. Then actually append the result the `list` called temp.
``` python
def appendToList(myFunc):
    if myFunc != None:
        temp.append(myFunc)
```
That is it! All I had to do after that was pop that first `None`, form the list"---"cannot index empty list"---" 




[day3]: https://adventofcode.com/2023/day/3
