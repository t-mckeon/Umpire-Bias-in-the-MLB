# Umpire-Bias-in-the-MLB

Hello. Welcome to my investigation into the systematic biases of strike calling in the MLB. 

**My Qualm**

Akin to most every baseball fan, I believe that MLB home plate umpires consistently blow strike and ball calls against my team (Go Cubbies). While it is most likely not true that MLB umpires have it out for my team, it is true that human umpires are tasked with an impossibly difficult task in calling balls and strikes consistently. New pitch-tracking technology has given average fans proof of the umpire's errors, as broadcasts show real-time position data of pitches as they cross the plate. This project seeks to take advantage of this pitch-tracking in the aggregate, in search of consistent biases MLB Umpires show, looking into possible home feild advantages given, advantages for righty or lefty hitters, and the squeezing of the zone on 2-strike counts and in extra innings.

Picutre - Ball called on close call in a two-strike count

**Data **

The data for this project comes from https://baseballsavant.mlb.com/statcast_search. Statcast has been tracking every pitch in the MLB and their results since 2008. Pitch data from each year is available in the Data Folder. This project uses the combined sheet from 2008-2021.

**Lets Get Started**

First, let's load in all #NUMBER OF PITCHES thrown between 2008 and 2021. We'll filter out pitches that were swung at, leaving pitches in need of a ball or strike call from the home plate uppire

Picture - all_pitches.svg

We can see that the umpires behind the plate are far from perfect in calling balls and strikes. But we'll need a more sophisticated measurement tool than our eye. To do this we'll use a combination of a Logistic Regression Model and a contour plot. 

Logistic Regression Model Formula

Picture - Pitches Plotted with hue as the predicted variable (0.0-1.0)

Contour Plot Explanation, with measurement of circles

Picture - Contour Plot on top of hue picture

For additional information, I added the classic 9-zone breakout of the MLB strikezone, and the percentage of pitches in each zone that were correctly called a strike. Here is the breakout for all pitches from 2008-2021.

Picture - 9-zone breakout

Using these new visualization tools, we can breakout the data into different situations and clearly show the systematic biases that exist among MLB home plate umpires. Here are a few of the most striking. 

Pictures - 2-strike count vs. Non
Pictures - Extra-Innings vs. Non
