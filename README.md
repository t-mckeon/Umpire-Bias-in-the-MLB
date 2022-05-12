# Umpire-Bias-in-the-MLB

Hello. Welcome to my investigation into the systematic biases of strike calling in the MLB. 

## My Qualm

<img align="right" src="https://user-images.githubusercontent.com/105253832/168170520-449b412b-548a-4a18-9c60-8ee9a2366cc6.svg" width="400" height="400">
Akin to most every baseball fan, I believe that MLB home plate umpires consistently blow strike and ball calls against my team (Go Cubbies). While it is most likely not true that MLB umpires have it out for my team, it is true that human umpires are tasked with an impossibly difficult task in calling balls and strikes consistently. New pitch-tracking technology has given average fans proof of the umpire's errors, as broadcasts show real-time position data of pitches as they cross the plate. This project seeks to take advantage of this pitch-tracking in the aggregate, in search of consistent biases MLB Umpires show, looking into possible home feild advantages given, advantages for righty or lefty hitters, and the squeezing of the zone on 2-strike counts and in extra innings.

## Data

The data for this project comes from [Statcast's Baseball Savant Database](https://baseballsavant.mlb.com/statcast_search). Statcast has been tracking every pitch in the MLB and their results since 2008. Pitch data from each year is available in the Data folder. This project uses the combined sheet from 2008-2021.

Selected dataset column meanings:
- pitch_name: Type of Pitch
- plate_x: Horizontal position of the ball when it crosses home plate from the catcher's perspective, normalized for lefty/right batters. (value of ball crossing left side of plate = 1.5, value of ball crossing right side of plate = 3.5)
- plate_z: Vertical position of the ball when it crosses home plate from the catcher's perspective, adjusted for height of batter. (value of ball crossing bottom of the zone = -0.725, value of ball crossing top of zone = 0.725)
- description: Result of pitch (called strike, swinging strike, ball, in-play, etc.)
- stand: Side of the plate batter is standing
- For other column descriptions, see the [Stacast Documentation](https://baseballsavant.mlb.com/csv-docs)

## Lets Get Started

First, let's load in all 5.2 million pitches thrown between 2008 and 2021. We'll filter out pitches that were swung at, leaving pitches in need of a ball or strike call from the home plate umpire.

<img src="https://user-images.githubusercontent.com/105253832/168170766-8dd49260-a635-4e60-925e-a81a6e43946c.png" width="500" height="500">

We can see that the umpires behind the plate are far from perfect in calling balls and strikes. But we'll need a more sophisticated measurement tool than our eye. To do this we'll use a combination of a Logistic Regression Model and a contour plot. 

Logistic Regression Model Formula

<img src="https://user-images.githubusercontent.com/105253832/168171042-d9f528a8-edc4-46f5-b5f8-465c39831e03.png" width="500" height="500">

Contour Plot Explanation, with measurement of circles

<p float="left">
<img src="https://user-images.githubusercontent.com/105253832/168171098-a9852550-e4ba-43bd-a3b3-b40a5cc8e13d.png" width="500" height="500">
<img src="https://user-images.githubusercontent.com/105253832/168171232-173b59b6-8409-43e6-84c5-db5dc0406213.svg" width="500" height="500">
</p>

For additional information, I added the classic 9-zone breakout of the MLB strikezone, and the percentage of pitches in each zone that were correctly called a strike. Here is the breakout for all pitches from 2008-2021.

Picture - 9-zone breakout

Using these new visualization tools, we can breakout the data into different situations and clearly show the systematic biases that exist among MLB home plate umpires. Here are a few of the most striking. 

<p float="left">
<img src="https://user-images.githubusercontent.com/105253832/168164448-45386ea3-2622-4539-a62d-21e75e1205aa.svg" width="500" height="500">
<img src="https://user-images.githubusercontent.com/105253832/168164516-c4127e96-151e-4ceb-8b5e-8bdf05029f56.svg" width="500" height="500">
</p>

<p float="left">
<img src="https://user-images.githubusercontent.com/105253832/168165777-685cde0c-30b7-4ad0-a9d8-dd91ad0f51c6.svg" width="500" height="500">
<img src="https://user-images.githubusercontent.com/105253832/168165820-36c5362e-3990-4c76-9bd5-64fe27ddea17.svg" width="500" height="500">
</p>
