---
draft: false
tags:
  - collage
  - datasci
date: 9/5/2024
---
# [my magnum opus of summer 2024](https://joelleneyap-fandom-streamlit-welcome-fli9ev.streamlit.app/)
I may never get over how proud I am of this project! I used **Social Network Analysis on [data](https://archiveofourown.org/admin_posts/18804) from fanfiction website Archive of Our Own** in March 2021. This project focuses on crossovers by drawing links between fandoms when they're tagged together in at least one hundred works, and plots graphs that visualize the interconnected relationships between fandoms and their communities.

I made **two apps on Streamlit**! and taught myself Streamlit & Pyvis graph embedding while I was at it — on top of bokeh and NetworkX from previous [[datasci]] adventures.

## [The Crossover Network](https://joelleneyap-fandom-streamlit-welcome-fli9ev.streamlit.app/Crossover_Networkx)
This applies the NetworkX ego graph method to a single node/fandom in the AO3 dataset, showing the entire network of crossovers with that fandom. A link will be represented when two fandoms have been tagged together in over 100 works. 
![[Sep-04-2024 16-19-21.gif]]

This even allows interactivity! You can search for fandoms you're interested in, see the count of works on AO3, choose one, set the range of the number of neighboring nodes you'd like to see, and see the graph change! ![[Sep-05-2024 12-58-51.gif]]

## [The MCU Number Game](https://joelleneyap-fandom-streamlit-welcome-fli9ev.streamlit.app/MCU_Number)
I've been so inspired by [The Oracle of Bacon](https://oracleofbacon.org/help.php) that I decided to make something similar. It turns out that the Marvel Cinematic Universe is the most well-connected node / the fandom included in the most number of crossovers with other fandoms. That begs the question: which fandoms don't have crossovers with the MCU? What are the fandoms connected to the MCU by the longest chain of crossover pairs?

I challenge users to find a fandom with the highest MCU Number (the smallest number of links a given fandom is away from the MCU) OR one that has no crossovers with it at all. Be on the lookout for little easter eggs when you're successful! 
![[Screenshot 2024-09-05 at 12.38.11 PM.png]]

If you want to know the answers... DM me on [Twitter](https://x.com/hug_starved).