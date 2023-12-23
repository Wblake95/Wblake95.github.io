---
layout: post
title: My first post! Bash functions for post variables
date: 2023-12-23 14:42:21 -0800
categories: jekyll bash 
---

# My first post! Bash functions for post variables.

## My problem
I just started with Jekyll today for blog posting. I knew that creating the environmental variables was going to get annoying really quickly, so, in comes bash to the rescue.

## What I did
I first attempted to do an alias, but I realized that I was going to be more complicated because I might have to add more steps. This led to bash functions. For now, I just need these basic variables,
* layout
* title
* date
* categories
From here, I only needed two variables to be past, date and a post name, that is just `$1` and `$date`.

## My solution!
{% highlight bash %}
function post() {
    echo "---
    layout: post
    title: $1
    date: $(date +%Y-%m-%d) $(date +%H:%M:%S) -0800
    categories:
    ---" >> ~/Documents/.scripts/Wblake95.github.io/_posts/$(date +%Y-%m-%d-)"$1".md
    vim ~/Documents/.scripts/Wblake95.github.io/_posts/$(date +%Y-%m-%d-)"$1".md
}
{% endhighlight %}
