---
layout: post
title: Wine spend and academic performance
description: "Wine budget and academic performance at Cambridge University."
category: articles
image: 
  thumb: wine_thumb.png
  homepage: wine_thumb.png
tags: [R, Wine,Cambridge University]
comments: true
share: true
---

About a week ago a good friend of mine, Tim, showed me a link to an economist blog post[^1]
 that plotted the wine budget of Cambridge Colleges. The figure from that blog post is below.

<figure>
	<a href="/images/wine.jpg"><img src="/images/wine.jpg"></a>
	<figcaption>The well travelled plot mentioned by the ecominist.com (THIS PLOT IS NOT BY ME).</figcaption>
</figure>
 
 Below, I took the data from the original plot above, and rendered it as an interactive
  javascript plot - hover over a point to see the college info.
  The author of the original plot used a log scale. Which fit the model better, but obscured 
  just how much money King's, John's and Jesus spend.
  
  *I'll slowly post all the code for all the plots and regressions past this point as I get the time to
 tidy up the syntax.*

<html>
  <head>
    
    <script src='http://ramnathv.github.io/rCharts/libraries/widgets/polycharts/js/polychart2.standalone.js' type='text/javascript'></script>
    
    <style>
    .rChart {
      display: block;
      margin-left: auto; 
      margin-right: auto;
      width: 550px;
      height: 400px;
    }  
    </style>
    
  </head>
  <body>
    <div id='chart38dc461cfd8b' class='rChart polycharts'></div>  
    
    <script type='text/javascript'>
    var chartParams = {
 "dom": "chart38dc461cfd8b",
"width":    550,
"height":    400,
"layers": [
 {
 "x": "Wine_budget",
"y": "Firsts_2013",
"data": {
"Wine_budget": [ 71055, 87685, 79989, 79254, 77798, 131127, 23028, 30051, 96994, 27975, 14034, 212256, 338559, 68192, 32917, 27263, 141692, 82133, 111113, 44722, 49498, 97507, 62432, 19304, 260064, 223292, 127186, 39647 ],
"Firsts_2013": [   24.7,   28.3,   25.3,   23.9,     23,   30.5,   21.4,   18.5,   21.1,     16,   13.2,   27.1,   25.9,   22.8,   13.9,   15.8,   33.7,   27.8,   26.3,   16.2,   21.6,   19.8,   26.9,   13.4,   25.1,   41.7,   28.1,   18.9 ],
"College_char": [ "Christ's", "Churchill", "Clare", "Corpus Christi", "Downing", "Emma", "Fitzwilliam", "Girton", "Caius", "Homerton", "Hughes Hall", "Jesus", "King's", "Magdalene", "Murray Edwards", "Newnham", "Pembroke", "Peterhouse", "Queens", "Robinson", "Selwyn", "Sidney", "St Catharine's", "St Edmund's", "St John's", "Trinity", "Trinity Hall", "Wolfson" ],
},
"facet": null,
"type": "point",
"width":    500,
"color": "College_char" 
} 
],
"facet": [],
"guides": {
 "y": {
 "min":      0,
"max":     40,
"title": "% with firsts" 
},
"x": {
 "min":      0,
"max":  4e+05,
"title": "Yearly wine budget in millions (£)" 
},
"color": {
 "numticks": 28,
"labels": [ "Caius", "Christ's", "Churchill", "Clare", "Corpus Christi", "Downing", "Emma", "Fitzwilliam", "Girton", "Homerton", "Hughes Hall", "Jesus", "King's", "Magdalene", "Murray Edwards", "Newnham", "Pembroke", "Peterhouse", "Queens", "Robinson", "Selwyn", "Sidney", "St Catharine's", "St Edmund's", "St John's", "Trinity", "Trinity Hall", "Wolfson" ] 
} 
},
"coord": [],
"id": "chart38dc461cfd8b" 
}
    _.each(chartParams.layers, function(el){
        el.data = polyjs.data(el.data)
    })
    var graph_chart38dc461cfd8b = polyjs.chart(chartParams);
</script>
    
  </body>
</html> 

Now I'm going to add a disclaimer - **this is not a robust analysis**. I removed Lucy,
 and the grad only colleges (as they don't get ranked), and I am purposely ignoring college
 assets. It seems the money a college has is hugely associated with academic performance, and 
 there is a large degree of multi- collinearity with their wine spend. Which would completely
 ruin my chance to run some models and make some plots.

So - with that out of the way, how are the characteristics of the colleges correlated?
 Below is plot from *ggpairs*, that automatically produces two pairwise plots for every variable.

<figure>
	<a href="/images/wine_1_scattermatrix.png"><img src="/images/wine_1_scattermatrix.png"></a>
	<figcaption>Scatterplot matrix of pairwise correlations. Plot type is defined by data in each pair.</figcaption>
</figure>

So the Tompkins Score[^2] has a near perfect correlation with percent firsts. As the score is
 based on undergrad results, this makes sense. More interesting is that there is a pretty 
 good correlation between the younger a college is and the worse it's students perform (see inside 
 the blue boxes). Below is just the continuous variables in a scatterplot by the *corrgram* function. 
 The red line with an ellipse is a Loess smoothed line (like an average) with a 68% concentration
 eclipse. You can interpret this as; inside the ellipse, that red line is a fairly good indication 
 of the association between the two variables.

<figure>
	<a href="/images/wine_2_scattermatrix_corrgram.png"><img src="/images/wine_2_scattermatrix_corrgram.png"></a>
	<figcaption>Scatterplot using an alternative plotting function (this one can't handle categories as well).</figcaption>
</figure>

So going back to wine spend vs. percent with firsts - is it just that bigger colleges spend more?

<figure class="half">
	<img src="/images/wine_3a_wine_firsts.png">
	<img src="/images/wine_3b_wine2people_firsts.png">
	<figcaption>On the left is the raw wine budget, on the right the x-axis is wine per college member.</figcaption>
</figure>

The plot above suggests no. So what would the regression models look like? 

### y ~ x

In the most basic model, a linear regression of % with firsts against the wine budget
 (actually using the natural log of the wine budget in the model),
 
 * 61% of the variation is explained by the model
 * wine budget effect is significant (p=0.000001)
 * and going from spending £50,000 a year to £100,000 a year on wine results in the proportion of students getting a first going from 21.2% (95%CI 12,30) to 28.0% (95%CI 19,37).
  
### y ~ x + z

A model where I've used Ordinary Least Squares (OLS) regression to attempt to adjust for the
 number of college members, the age of the college, and the proportion that are female.
 There are a lot of caveats here - there is no obvious causal pathway. Loosely, an 
 older college is more likely to have amassed a lot of assets, and have the capacity to get into 
 wine speculation. Female dominated colleges, by virtue of there being no females at Cambridge 
 in the far too recent past, are likely to be young colleges.[^3]
 
I've also ignored a few other variables - I won't go into details, but I did a (lazy)
 forward selection, basing my decision mainly on how the coefficients moved as variables
 were added.
 
So, while the conceptual underpinnings of this are a mess.... 
what do the numbers look like if I attempt to adjust out 
 the effect of the number of members in the college, it's age, and the percent female?
 
 The results of this adjusted model are,
 
 * 65% of the variation is explained by the model
 * wine budget effect is significant (p=0.00752)
 * and going from spending £50,000 a year to £100,000 a year on wine results in the proportion of students getting a first going from 21.8% (95%CI 13,31) to 26.6% (95%CI 18,36).
 
<figure>
	<a href="/images/wine_5_ModelResiduals.png"><img src="/images/wine_5_ModelResiduals.png"></a>
	<figcaption>Residuals from the adjusted OLS model.</figcaption>
</figure>

Above is a summary of the model fit. It's not perfect, and a few colleges stand out as not fitting
 particularly well. Interesting here is that two colleges in particular hold a lot of sway in the 
 model. A common rule of thumb is that if an observation has a Cook's distance greater than four 
 divided by your total number of observations, your analysis is unstable. 
 
Using that rule, there are two colleges that are very influential to my results. Homerton
 and Trinity. It's easy to see why. Homerton is mainly female (63%), is 38 years old, performs badly 
 (16% get firsts) and spends about £20 per member a year on wine. While Trinity is mainly male (37% female) 
 is 468 years old, has exceptional under grads (42% get firsts) and spends £179 per member a year on wine.
 
Another way to look at this is the influence plot, below.
 
 <figure>
	<a href="/images/wine_influence.png"><img src="/images/wine_influence.png"></a>
	<figcaption>A “bubble” plot of Studentized residuals by hat values, with the areas of the circles representing the observations proportional to Cook's distances. Vertical reference lines are drawn at twice and three times the average hat value, horizontal reference lines at -2, 0, and 2 on the Studentized-residual scale.</figcaption>
</figure>
 
So what is the effect of these variables I'm trying to adjust out? Below is an Added Variables Plot (AVP).
 This plot shows the effect of adding in a new variable, if the others are already in the model.
 This shows the positive relationship between age of college, wine budget, and number of people,
 and the negative association between percent female and performance.


<figure>
	<a href="/images/wine_4_AVP_WinePerAgeFem.png"><img src="/images/wine_4_AVP_WinePerAgeFem.png"></a>
	<figcaption>Added variable plot.</figcaption>
</figure>

So there are outliers, and I don't really have a valid reason for excluding them. Two ways
 to dampen the effect of outliers is robust and quantile regression. Adjusted results are below,

### Quantile regression
 
 * Going from spending £50,000 a year to £100,000 a year on wine results in the
  proportion of students getting a first going from 21.4% to 26.3%.
 
### Robust regression 
 
 * Going from spending £50,000 a year to £100,000 a year on wine results in the proportion 
 of students getting a first going from 21.5% to 25.9%.
 
 And finally, all the models looking at wine budget vs. percent with firsts, plotted together.

<figure>
	<a href="/images/wine_6_comparemodels.png"><img src="/images/wine_6_comparemodels.png"></a>
	<figcaption>Added variable plot.</figcaption>
</figure>

[^1]: The graph was actually by a Cambridge grad, but the economist [post is here.](http://www.economist.com/blogs/freeexchange/2014/02/correlation-and-causation)
[^2]: The Tompkins score allocates 5 points for a First Class degree, 3 points for an Upper Second (known also as a 2.i), 2 points for a Lower Second (a 2.ii), 1 point for a Third and no points for someone only granted an allowance towards an Ordinary Degree.
[^3]: This also suggests I maybe should of looked at female as binary (all female or mixed).