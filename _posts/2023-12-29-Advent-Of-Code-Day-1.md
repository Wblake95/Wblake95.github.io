---
layout: post
title: Advent-Of-Code-Day-1
date: 2023-12-29 07:14:05 -0800
categories:
---
# Advent of Code day 1
I completed the first day of Advent of Code. The first part was extremely easy. However, I struggled with the second part. I thought my idea to use a dictionary to store the string index as the key and value as the value was brilliant.

# What I did, 
1. saved the file as plain text, as usual
2. python function `open with`
3. `for` loop each line
4. use `find` and `rfind` to locate my answers. (where the problem was)
5. combine both as strings and add the final answer.

# How I solved it
My idea was brilliant, I just fell into a classic problem, repeating myself! I wrote the code for `find` and `rfind` twice in the same if statement! Since I use vim, I just copied the if statement 4 times and changed the first line. Below, you can see the final product. I assigned the function to a variable and just used it when I needed it.
You can see all of my code on my [github][Wblake95]
``` python
for i in file:
    temp = {}
    low = ""
    high = ""
    for j in nums:
        begNum = i.find(str(j))
        if begNum != -1:
            temp.update({begNum:j})
    for j in nums:
        endNum = i.rfind(str(j))
        if endNum != -1:
            temp.update({endNum:j})
    for k in spelledNums:
        begSpell = i.find(k)
        if begSpell != -1:
            temp.update({begSpell:spelledNums[k]})
    for k in spelledNums:
        endSpell = i.rfind(k)
        if endSpell != -1:
            temp.update({endSpell:spelledNums[k]})
    low = min(temp.keys())
    high = max(temp.keys())
    temp = str(temp[low]) + str(temp[high])
    answer += int(temp)
print(answer)
```
[Wblake95]: https://github.com/Wblake95/pythonLearning/tree/main/advent-code
