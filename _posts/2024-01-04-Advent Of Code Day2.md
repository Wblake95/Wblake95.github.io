---
layout: post
title: Advent Of Code Day2
date: 2024-01-04 14:34:36 -0800
categories:
---
### Day 2!!!
I completed the second day of Advent of Code! Again, the first part was rather easy. But, the second part I changed it up to try a match case, for the experience. I also got tired of doing so many splits, so I went with a regex search for each line on both parts 1 and 2.

## What I did,
# part 1
1. Save the file as plain text, as usual
2. Python function `open with`
3. It was a two `for` loops and two `if` statements

# part 2
1. Same as steps 1 and 2 from part 1
2. I started with regex instead of a million splits
3. Made a couple lists for each color
4. Added to the score without issue

## How I solved it (day 1)

I was originally doing list, but I got two list deep and needed another, from that point I knew this was the worst way to do this. The first thing that came to bind was regex. I gave it a shot and nailed it on the first try. This is what it looked like.
``` python
import re
x = re.findall("\d+ [r|g|b]", i)
```
After that, it gave a list of each color and its number, for example ["1 r", "2 g", "3 b"]. I then did my second for loop to iterate over the list and split, temporarily, to check the number and color. It worked perfectly!
I then added a simple Boolean toggle in a variable called temp and added my first if statement that would toggle temp each time the number exceeded its color equivalent, since that sample wouldn't be possible.
``` python
check = {
    "r": 12,
    "g": 13,
    "b": 14
    }
for j in x:
    a = j.split(" ")
    if check[a[1]] < int(a[0]): # example: check[key] < value
        temp = False
        break
if temp:
    x = re.search("^Game \d+", i)
    a = x.group()
    a = a.split(" ")
    score += int(a[1])
```
Finally, all I had to do was check if temp was true and find the "game number". I just did that was another regex search, a split, and convert that string to and int and I was done.

## How I sovled it (day2)

For this problem, I just needed to multiply the highest number of each color per game and add that total to a variable I called score. However, I skipped the `dictionary` and went for three list, one for each color. I kep the regex I had from the previous part and did a `match case` instead, for the experience. The code itself isn't all that interesting, but I learned alot. For example, you can't use a variable for the case unless it is the defualt. I new that `_`, was used as the defualt, but that can acutally be any thing.
``` python
match a[1]:
    case "r" if check >= red[0]:
            red[0] = check
    case "b" if check >= blue[0]:
            blue[0] = check
    case "g" if check >= green[0]:
            green[0] = check
    case _:
        print("Check", check, "num, color", a)
```
As you can see, your match can be a variable, but I had to change the each case to a string to make it work. However, you can throw in an `if` statement to make it match a condition as well. You can be the judge if that is more Pythonic or not.

You can see all of the code on my [Github][github]

[github]: https://github.com/Wblake95/pythonLearning/tree/main/advent-code
