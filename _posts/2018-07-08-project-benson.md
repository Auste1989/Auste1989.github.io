---
layout: post 
title: The Very First Project @Metis
quote: We need women at all levels, including the top, to change the dynamic, reshape the conversation, to make sure women’s voices are heard and heeded, not overlooked and ignored - Sheryl Sandberg, Facebook COO
image:
      url: /media/2018-07-08-project-benson/cover.jpg
---

## Intro:
A New York based organization called WomenTechWomenYes (WTWY) has reached out to my team asking for help. As an NGO (Non-Governmental Organization) they mostly depend on donations from members and the general public. Every year WTWY organises an Annual Summer Gala to increase awareness of gender diversity gaps in technology industry and raise funds that will allow them to continue inspiring women to take on the challenge and succeed in various tech roles (such as Data Scientists or Data Engineers).
The organization mostly relies on volunteers to promote their annual events, they would like to optimize the allocation of their flyer distributing street teams in order to maximize the signups and, in turn, the attendance and donations. Without further ado, we took on the challenge! 

## How we did it: 
* Split our team into sub-teams (New York subway station (MTA) Data, Google Maps API, Visualization)
* Scraped MTA data from their website
* Explored, cleaned and analysed it
* Generated a list of stations with the highest passenger velocity
* Based on the list of stations, queried Google Maps data of nearby Tech companies and Starbucks coffee shops
* Used Census demographics data to identify areas with more female residents
* Scored each station based on above criteria
* Depicted results on the New York map (using GeoPandas)
* Provided WTWY with a general recommendation for Top 20 stations to focus on
* Additionally, created a tool that will allow a quick allocation of resources based on weekday and hour

## What we discovered:
As our target audience, we have chosen a young woman called Becky, who is in her 20s /  30s, works for a tech company and loves Starbucks coffee. Given this profile, we matched up the highest velocity stations with distance to the nearest Tech companies, Starbucks coffee shops and residentials areas with a higher women to men ratio.   
As an example, even though Flushing Main street station had higher passanger velocity than 59 St. and Columbus Circle, the latter was ranked higher due to it's proximity to large tech companies and Starbucks coffee shops. 
Our results suggested that teams should be positioned around the stations in Lower Manhatten, such as Times Sq and 42 St or East 14th St, as well as a couple of stations in Brooklyn and Queens.  

**Heatmap of the busiest New York subway stations**  
![Image Missing]({{"/assets/subway_plot.png"|https://github.com/Auste1989/Auste1989.github.io/blob/master/assets/subway_plot.png}})

**Final Top 10 Recommended Stations**   

![Image Missing]({{"/assets/Final Recommendation Map.png"|https://github.com/Auste1989/Auste1989.github.io/blob/master/assets/Final%20Recommendation%20Map.png}})

### I bet Your organization could also use data science driven analysis to gain competitive advantage! Please do not hesitate to reach out to discuss potential work this team could do for You!

