---
tags:
  - page
date: 8/21/24
draft: true
title: "[DSxAO3] 4: Crossover Network"
---
This was actually the next thing I wanted to work on after doing [[DSxAO3, 2; Character Social Network]], partly because I wasn't really satisfied with the way it showed ships. Nodes were often entirely stacked on top of each other to form one 'node pairing' representing a ship, because of how often some characters were shipped with others. I realized what I actually wanted to see was contingent on the fandom — whether some had denser relationships than others. That led me to think about crossovers! Because I think the most interesting outcome of the above experiment would have been to see characters shipped together but from two different fandoms, like Harry Potter x Loki for example.

So this time:
* each node is a fandom
* an edge is defined as the existence of a crossover fic between two fandoms/nodes
* the darker the color, the greater the number of fics within that fandom
* the larger the circle for the node, the higher the degree of that node

![[Screenshot 2024-08-21 at 4.22.23 PM.png]]

As always, interactive code [here](https://deepnote.com/workspace/ao3-cdb24469-2834-4827-96fb-17793ac7554f/project/AO3-x-NetworkX-ebe988dc-072f-4e99-a43e-95707726522c/notebook/AO3%3A%20networkx-03b703c2181e4ca8b2f0c873f2ca863f) — scroll down to "Crossover Network" — and Github code [here](https://github.com/joelleneyap/fandomstudies/blob/main/fandom_networkx.ipynb). 

Took some work to count every instance of two or more fandoms being tagged for a given piece of fanfiction:
* Removed all redacted fandoms
* Removed edges between fandoms and "anime - fandom" and other possibilities
* Dropped all combinations of BnHA, boku no hero academia, MHA, my hero academia etc
	* Don't know why there were so many of these, with works tagging different permutations of the different names for [BnHA](https://myheroacademia.fandom.com/wiki/My_Hero_Academia_Wiki). There's probably lots more like this, but nothing else I could see that had such high counts

At this point, I reach that perpetual problem of having too many rows to graph. So I made two graphs with two different approaches!

## Random sample
For the first one, I take a random sample of 50 edges between fandoms, from those with more than 100 crossover fics written.

![[fandom network sample.gif]]

It takes a random sample every time the code is run, so feel free to go into the [Deepnote](https://deepnote.com/workspace/ao3-cdb24469-2834-4827-96fb-17793ac7554f/project/AO3-x-NetworkX-ebe988dc-072f-4e99-a43e-95707726522c/notebook/AO3%3A%20networkx-03b703c2181e4ca8b2f0c873f2ca863f) and play around with different samples! I really love this one because you can see expected pairs like "Star Wars - All Media Types" and "Star Wars Legends: Knights of the Old Republic", but also less expected ones like "Harry Potter - J.K. Rowling" and "James Bond (Craig movies)". 

### A note on degrees
Every hover-over has the name of the fandom, the degree of the node, and the count of the number of fics tagged with that fandom. From NetworkX, [degree](https://networkx.org/documentation/stable/reference/classes/generated/networkx.Graph.degree.html) is: 
> The node degree is the number of edges adjacent to the node. The weighted node degree is the sum of the edge weights for edges incident to that node.

This, of course, only applies to the nodes in the sample of 50. That's why the degrees seen in the visualization are so much lower than what you'd expect — "Naruto" has a degree of 1, where it's overlapped with "Katekyō Hitman Reborn!", but I know for sure that there are crossovers between "Naruto" and "Harry Potter". It's just that that particular edge between these 2 fandoms weren't sampled. 

So sampling this way isn't really representative. It makes the fandoms represented seem more intertwined with one other fandom (like "Naruto" and "Katekyō Hitman Reborn!") than they actually are. What are other ways to do this?

## Top 50 Crossovers
![[fandom network top 50.gif]]

Yeah, I know it looks like cartoon Mars.

This took a little more filtering than I thought it would. Here's a part (15 rows) of the original top 50 crossover edges:
![[Screenshot 2024-08-21 at 4.58.23 PM.png]]

It's clear that there's a lot of MCU on here. But more importantly, a lot of these 'crossovers' are just when a work is tagged with multiple versions of the same fandom, e.g. The Avengers (Marvel) - All Media Types and The Avengers (Marvel Movies). But! This doesn't mean that 2 tags with "All Media Types" could come together to be a crossover from 2 different fandoms. It's just more common for the bigger fandoms to have the possibility of tagging "All Media Types". 

I'm more interested in crossovers between fandoms though, so I decided to remove rows that mention "All Media Types" and "& Related Fandoms".

Here's what it looks like with the node size detached from degree: 
![[Screenshot 2024-08-21 at 5.06.17 PM.png]]

Upon further investigation though, other than that huge stack of nodes in the middle that's the MCU and related movies/shows/comics, the nodes are mostly still stacked on top of each other in paired clumps. 

## Re-orient: Ego networks
Maybe what I want is the ego network of a single node!