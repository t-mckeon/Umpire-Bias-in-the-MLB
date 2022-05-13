# Umpire-Bias-in-the-MLB

Hello. Welcome to my investigation into the systematic biases of strike calling in the MLB. 

## Inquiry

<img align="right" src="https://user-images.githubusercontent.com/105253832/168171958-4ca26c14-b1f9-40ae-8cad-3d78826b7779.svg" width="400" height="400">
Human umpires are tasked with the important yet extremely difficult task in deciding whether the hardest thrown and nastiest pitches in the world are strikes or not. With motion technology, TV audiences are now shown the actual path of a pitch on close calls, ousting human home plate umpires as inconsistent and faulty in their judgements. This project seeks to take advantage of this pitch-tracking in the aggregate, in search of consistent biases MLB Umpires have in their strike calling.

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

First, let's load in a sample of 520,000 pitches thrown between 2008 and 2021. We'll filter out pitches that were swung at, leaving 501,038 pitches in need of a ball or strike call from the home plate umpire.
<p float="center">
<img align="center" img src="https://user-images.githubusercontent.com/105253832/168170766-8dd49260-a635-4e60-925e-a81a6e43946c.png" width="500" height="500">
</p>
We can see that the umpires behind the plate are far from perfect in calling balls and strikes. But we'll need a more sophisticated measurement tool than our eye. To do this we'll use a combination of a Generalized Additive Model and a contour plot. 

A Generalized Additive Model is a model in which the response variable depends on unkown smooth functions of predictor variables. With the goal of attempting to find a general strike zone from MLB umpires, interpretability of the coefficients of the model is not as important as creating a visual understanding of how balls and strikes are called. 

The Model looks like this: g(E(Y)) = B0 + f1(x1) + f2(x2), specified as a binomial distribution
- g(E(Y)) = Expected Result of Pitch - Closer to 1 = More likely to be called a strike, Closer to 0 = More likely to be called a ball
- x1 = plate_x, horizontal position of pitch as it crosses the plate
- x2 = plate_z, vertical position of pitch as it crosses the plate

After running the model and merging the predicted values to the origional data, we can visualize the results by assigning a colormap to the predicted value.

<img src="https://user-images.githubusercontent.com/105253832/168171042-d9f528a8-edc4-46f5-b5f8-465c39831e03.png" width="500" height="500">

We can start to see where MLB Umpires are most likely to call a strike, but we need to create a sharp edge to clearly view the bias. To do this, we'll treat the predicted values like altitute values on a map, and draw contour circles at the 50% "altitude (circle in the visualization that is white), in order to represent the points where MLB Umpires are equally likely to call a ball or a strike. This is represented by the black circle below, additionally let's add a contour circle at the 90% point to add some more information. 

<p float="left">
<img src="https://user-images.githubusercontent.com/105253832/168171098-a9852550-e4ba-43bd-a3b3-b40a5cc8e13d.png" width="500" height="500">
<img src="https://user-images.githubusercontent.com/105253832/168171232-173b59b6-8409-43e6-84c5-db5dc0406213.svg" width="500" height="500">
</p>

Finally, lets add one more visual aid. I added the classic 9-zone breakout of the MLB strikezone, and the percentage of pitches in each zone that were correctly called a strike. Here is the breakout for all pitches from 2008-2021.

<img src="https://user-images.githubusercontent.com/105253832/168391618-5185b2f8-e234-4e92-ad9c-f61fb994cf60.svg" width="500" height="500">


Using these new visualization tools, we can breakout the data into different situations and clearly show the systematic biases that exist among MLB home plate umpires. Here are a few of the most striking. 

<p float="left">
<img src="https://user-images.githubusercontent.com/105253832/168164448-45386ea3-2622-4539-a62d-21e75e1205aa.svg" width="500" height="500">
<img src="https://user-images.githubusercontent.com/105253832/168164516-c4127e96-151e-4ceb-8b5e-8bdf05029f56.svg" width="500" height="500">
</p>

Here we see a clear squeezing of the strikezone when the count has 2 strikes. This is an example of human bias - likely the umpire not wanting to ring up a batter on a close call - influencing the results of the game. For more, see the Umpire Bias in the MLB PDF report in this repository.
