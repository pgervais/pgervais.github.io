---
layout: post
title:  "A Tooling Tidbit"
date:   2024-02-10
categories: eng tidbits
---

A good recipe for a successful product is to reduce friction, that is **reduce mental load for the users**. It's something to be taken seriously: if your product requires too much mental effort, users will simply not use it.

This post is about a very small example that I stumbled upon while configuring my own environment.

I wanted to solve a minor but vexing problem (to me): how to create a directory using the shell and immediately cd into it. You probably don't see a problem here. This is how to do it:

{% highlight shell %}
some/dir$ mkdir new_dir
some/dir$ cd new_dir
some/dir/new_dir$ 
{% endhighlight %}

and it requires typing the directory name twice, which I found frustrating.

## Solution 1: autocompletion

Autocompletion makes it trivial to enter the name twice, right? 

Well... If you're dealing with a handful of directories, yes. If you're dealing with a lot of very similarly-named directories like timestamped ones (think `2023-11-10`, `2023-10-10`, etc.), not so much. Same story if the path is something like `../../../../home/myuser/tmp/stuff/todelete/new_garbage.txt`. Using copy-pasting is slow and clunky.

## Solution 2: custom shell function
A function called `mkcdir` in the shell that runs both `mkdir` and `cd`:

{% highlight shell %}
some/dir$ mkcdir new_dir
some/dir/new_dir$ 
{% endhighlight %}

This failed for another reason: you don't necessarily want to change directories every time. Otherwise you'd have aliased `mkdir` to this new function. `mkcdir` forces you to decide *ahead of time* whether to change the working directory. That turned out to be too much mental load to be practical.

**Side note**: It's very similar to the reason why Chrome ended up with a single text box to enter a URL and a search: having two distinct boxes - one for searching and one for a URL - was too much mental load.

## Solution 3: look back

Taking a step back, I realized that the issue wasn't the number of commands to type or the number of characters, but the fact that when typing `cd new_dir`, you're providing the shell with some information *you've provided on the line above*. So what I needed was a function that would say "change to the directory *I just created*". And that's quite easy by looking into the shell's history. 

Now we have a function called `ff` for "follow" - it also had to be easy to type - that just inspects the shell's history and extracts the last command's last argument. Then we can do:

{% highlight shell %}
some/dir$ mkdir new_dir
some/dir$ ff
some/dir/new_dir$ 
{% endhighlight %}

This function solved all the above problems, and more.

## Happy consequences
A sign that you've got a good solution is that it solves other problems. The same pattern applied to `ls`, `mv`, `cp`, `mkdir` and others:

{% highlight shell %}
some/dir$ mv image.png new_dir
some/dir$ ff
some/dir/new_dir$ 
{% endhighlight %}

Even the term "follow" was inspiring. Something that I also do every once and a while is to navigate to the directory pointed to by a symlink. Assuming that `link.txt` points to `../../other_dir/readme.txt`, now you can do:

{% highlight shell %}
some/dir$ ff link.txt
other_dir$ 
{% endhighlight %}

## Lessons learned
The above should have exemplified two principles:

- users should only need to provide information the computer does **not** already have. `ff` solves this problem by looking into the shell's history.
- avoid forcing decisions ahead of time. That was the flaw with the `mkcdir` solution: it was forcing the user to make a decision between `mkdir` and `mkcdir` every time. 
