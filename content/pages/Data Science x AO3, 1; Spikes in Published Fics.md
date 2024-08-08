---
draft: false
date: 7/30/24
tags:
  - page
title: "[DSxAO3] 1: Spikes in Published Fics"
---
Part 1/?

Post-college, pre-job: Was feeling like I was losing my skills and experience from college, so I decided to start up a personal project: Investigating the data from the [selective data dump for fan statisticians](https://archiveofourown.org/admin_posts/18804) that fanfiction archive site Archive of Our Own uploaded in March 2021. I've always wanted to do this and am so excited to share what I learn!

Everything I'm working on is documented in [this Github repo](https://github.com/joelleneyap/fandomstudies). A little messy but I'll clean as I go! Original CSVs were put up on the AO3 website [here](https://archiveofourown.org/admin_posts/18804): one for works and another for tags. 

## Investigating spikes in published fics over time
The first research question I had! What caused the sudden spikes in counts of fics published on specific days in the below graph?

All my DS classes have taught me to react to a dataset first with some exploratory data analysis, so that's what I did at the beginning. The works CSV from AO3 has a column called "creation date", the date a fic was posted on the site. I wanted to see if there was a trend in works created over time, so I graphed that out after converting the strings in there to datetime objects.
![[Screenshot 2024-07-19 at 5.20.15 PM.png]]

It seems like there's a general upward trend on number of fics published each day between 2009 to 2021. But what stands out are those three spikes in 2012, 2013 and 2014, as highlighted in the box above. 

#### Identifying dates of spikes
I could filter the list of works by the column "creation date", so I could use the specific dates that these spikes took place on as a lever to find out more. By setting bounds based on the graph above, I found local maximums within those bounds for the three spikes. Here's a code snippet:

```
early_2012 = works_dates.loc[(works_dates['date'] > '2012-01-28') &(works_dates['date'] < '2012-05-01')]
spike_2012 = early_2012[early_2012['works'] == max(early_2012['works'])]
print("Spike day in 2012: ", spike_2012['date'])
```

The spikes in fics published:
* 4752 works on 2012-03-05
* 6233 works on 2013-05-10
* 6732 works on 2014-05-16

These are really high compared to the average works published per day across the time period: 1605.14.

Next question: Why did so many authors publish fics on these dates? At this point, my hypothesis was that something major happened in the news regarding one or a few of AO3's most popular fandoms (e.g. Supernatural, Marvel, etc), and fanfic authors responded by writing and publishing more on these days. Alternatively, there could've been a writing event like Yuletide where authors would exchange fics and thus publish all at once.

For each spike date, then, I decided to try to find the list of works published on that date, and group by fandom to see if there were any trends.

### 2012-03-05
In the 'works' table provided by AO3, each row represents a work and has a list of tags in a column called 'tags'. However, these were just the IDs, which corresponded to the numbers in the column 'ID' of the 'tags' table. I had to do some cleanup and merging and ranking to get this:
![[Screenshot 2024-07-19 at 8.48.05 PM.png]]

At this point I started thinking that there's no way people put up 4.1k fics all for Smallville all on the same day, especially if the runner-up fandoms only have about 40 or less fics that day. 

4185 fics for Smallville, with 3853 out of those tagged Clark Kent/Lex Luthor. The date was 2012-03-05. It's strange: the Smallville TV series ended with Season 10 on May 13, 2011, long before March 2012. 

After looking around online, the only thing of note I could find in the news about Smallville between Feb 1, 2012, to March 5, 2012, was that [Season 11](https://m.imdb.com/news/ni22484166/) of the series would continue in a digital comic, picking up 6 months after the events of Season 10. Maybe the news of a beloved TV series being back gave a bunch of fic authors the inspiration to start again? Sounds implausible.

Then, I remembered seeing news on the AO3 homepage before, of an archive from somewhere else being imported onto AO3. I googled around for "Archive of Our Own" and "imported" around the date 2012-03-05, and hit the jackpot: [In March 2012,](https://fanlore.org/wiki/Smallville_Slash_Archive) the central archive for the Smallville fandom, the Smallville Slash Archive, was imported in! This was part of the Organization for Transformative Works' [Open Doors project](https://fanlore.org/wiki/Open_Doors), with a mission to preserve various at-risk fanworks on AO3 or by hosting fanworks directly. 

The Smallville Slash Archive hosted over 4000 stories as of 2010, and was mostly Clark/Lex fics. That matches! So the sudden addition of 4.1k fics to AO3 in 2012 was because fics were imported from an external source. That probably holds true for the other two, right?

### 2013-05-10
5431 fics, all for a fandom called The Sentinel.
![[Screenshot 2024-07-19 at 8.48.16 PM.png]]

That was honestly very surprising -- I was actually expecting a fandom that I was familiar with, but I'd never heard of The Sentinel before. Turns out it was an [American TV show that ran from 1996 to 1999](https://www.wikiwand.com/en/The_Sentinel_(TV_series)), about a cop with super-heightened senses and his roommate who teaches him how to use those senses. They fight crime together and also live together (hehe). Seeing as it's an old show that finished up way before 2013, this spike in fics posted was likely because of a similar reason to the Smallville Slash Archive. 

And yeah! It was! [852 Prospect](https://fanlore.org/wiki/852_Prospect), an archive for adult fanfiction for The Sentinel TV series, was imported to AO3 on May 10, 2013. It was named for the address that the two main characters, Blair and Jim, lived at on the show. 

I'm so happy to be doing this project because I find out interesting things like this: I knew I'd heard the word 'Sentinel' used in this context before, like a position or characteristic denoting some kind of superpower. From the Fanlore website for The Sentinel, there's a trope section that includes '[Sentinel AU](https://fanlore.org/wiki/Sentinel_AU)' -- a (romantic) trope where a character with superpowers is a Sentinel that needs a Guide to help them manage their powers, and the two are often 'fated for each other' in the way soulmates might be. It turns out that the Sentinel/Guide AU trope -- which I've seen in everything from Sherlock to Marvel -- *originated from* the fandom community and their fanfiction about The Sentinel. [Here](https://archiveofourown.org/tags/Alternate%20Universe%20-%20Sentinels%20*a*%20Guides/works)'s the AU tag on AO3 itself. That's so cool! Major piece of fandom history right there. The 852 Prospect legacy lives on!

### 2014-05-16
So there's a trend with the spikes being related to some other archive being imported to AO3, so there's probably the same thing here. Right? Well, kind of. 

Here's the list of fandoms with counts for fic put out on that day:
![[Screenshot 2024-07-19 at 8.48.35 PM.png]]

It's obvious that this is a different case now — the fics that are being added aren't from one specific fandom. Here's a bar chart with the top 20 fandoms from that day:
![[output 9.17.46 PM.png]]

I was stumped for like a whole day, because I kept googling "AO3", "imported" around the time of May 16, 2014, but kept coming up with nothing even though that worked for the previous 2 cases. I even made this little table that shows the top 5 dates with most fanfic posted on AO3 in 2014: 
![[Screenshot 2024-07-20 at 2.26.52 PM.png]]

Interesting that people post so much around Christmas! 'Tis the season, truly.

But! I was really convinced that it had to be that something was imported in to AO3 -- just that since it was spread across fandoms, it was maybe an archive that wasn't specific to a fandom, kind of like LiveJournal or Fanfiction.net.

So I gave up on googling and went back to AO3. I found the Organization for Transformative Works' homepage, and started going through their announcements page by page, all the way back to 2014. And finally! I found an [announcement](https://www.transformativeworks.org/yuletide-archive-move-complete/) put up on May 18, 2014. It stated that the [Yuletide Archive for 2003-2008](http://www.yuletidetreasure.org/) had finally been imported to AO3, again under the Open Doors project. 

What is [Yuletide](https://fanlore.org/wiki/Yuletide)? It's sort of like Secret Santa but for fic writers. It's an annual rare fandom gift exchange, usually for fandoms with less than x number of fics on AO3 or ff.net, depending on the rules that year. Participants enter by selecting a fandom and a set of characters, and commit to contributing a fic of more than 1,000 words that includes the characters in another participant's request. 

And it's because Yuletide is specifically focused on providing fics for rare fandoms and rare pairs, that the fic counts for 2014-05-16 in the first table in this section, just show the pretty much normal amounts of fic put out for the popular fandoms: Supernatural, MCU, Sherlock, etc. Because the jump on that day was mostly for rarer fandoms with less fic count, that wouldn't make it onto the 'top 5' ranking by counts that I made!

I leave you with the tail end of the fandoms with at least 1 fic published on that day -- the last 20 in the list. Some of these only have less than 5 fics on AO3 for the fandom total (that's the 'cached_count' column).
![[Screenshot 2024-07-20 at 2.34.44 PM.png]]

That's all for now! Next, I'm working on making an interactive social network graph with all characters on AO3, representing ships and crossovers in one visualization! So excited to stretch my NetworkX muscles once more.