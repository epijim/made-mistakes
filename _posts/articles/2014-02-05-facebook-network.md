---
layout: post
title: Plotting my Facebook data
description: "Plotting my Facebook data using R."
category: articles
tags: [R, Facebook,Network]
modified: 2014-02-11
image: 
  thumb: network_thumb.png
  homepage: network_thumb.png
comments: true
share: true
---

<figure>
	<a href="/images/network_1_mynetwork.png"><img src="/images/network_1_mynetwork.png"></a>
	<figcaption>Connections between my facebook friends.</figcaption>
</figure>
 
The plot above is a network of my Facebook friends that are friends with other.
 It’s quite cool how friendship circles stand out pretty clearly based on mutual friends. 
 I didn’t want to post the version with peoples photos/names, but the natural groupings in 
 the network match up pretty well with the labels I gave each group.

The colours of each node are based on betweenness[^1] – which I think means; if you draw the
 shortest line through the network between every 2 points, the colour represents 
 how many times the lines pass through each point (white=lots, red=none). 
 So the white dots are people that are ‘gateway’ friends. 
 It’s easy to see in my family – my mum (top white dot in family group) forms a connection 
 between my family and my closer uni friends. While my Aunti V, bottom right white dot, is 
 the only person amongst my Kiwi family who is FB friends with my extended Canadian and 
 Sri Lankan family.

The shape of this graph has been determined by an algorithm, which I choose post hoc.
 I then manually changed the ‘attractiveness’ of each node to move the people apart a bit. 
 Choosing a different algorithm to make the graph can have pretty drastic effects on how 
 the graph looks. An example what this data looks like using four different algorithms, 
 with all the optional variables that influence the graph left at their defaults, is below.

<figure>
	<a href="/images/network_2_types.png"><img src="/images/network_2_types.png"></a>
	<figcaption>Examples of my network plotted with four different algorithms.</figcaption>
</figure>

The plot below, which uses the KK algorithm, gives a better impression of how these
 groupings are just a subjective summary of where I feel the majority of the people in 
 each cluster come from.
 
 <figure>
	<a href="/images/network_3_detailed.png"><img src="/images/network_3_detailed.png"></a>
	<figcaption>Examples of my network plotted with four different algorithms.</figcaption>
</figure>

The relatively recently released *RFacebook* package allows you to tap into Facebook API,
 making graphs like above pretty easy to make. Most of the code here comes from this blog. 
 Setting up the access token is a little fiddly (if you don’t set up an app access only 
 lasts for 2 hours).

Below is a histograph of the ages of my Facebook friends (or at least their recorded ages).

 <figure>
	<a href="/images/network_4_age.png"><img src="/images/network_4_age.png"></a>
	<figcaption>Age distribution of my Facebook friends.</figcaption>
</figure>

The vast majority of my friends don’t have their relationship status up on Facebook,
 meaning you can’t pick up much from the plot below (red=a female, black= a male).
 
<figure>
	<a href="/images/network_5_relations.png"><img src="/images/network_5_relations.png"></a>
	<figcaption>Relationship status of my Facebook friends (majority do not have this entered).</figcaption>
</figure>
 
You can also pull stats on public pages. For instance,

* MCR Ents (my college social page): most popular post had 3 likes
* Cambridge Brewhouse (pub on my street):  most popular post had 16 likes and 2 comments
* Archer (TV show): most popular post was this video, and it had 73,013 likes, 2146 comments and 9315 shares.
* Below is a plot of the total comments, likes and shares for posts by the Jesus Bar since the page was launched. 

<html>
  <head>
    
    <script src='http://code.jquery.com/jquery-1.9.1.min.js' type='text/javascript'></script>
    <script src='http://code.highcharts.com/highcharts.js' type='text/javascript'></script>
    <script src='http://code.highcharts.com/highcharts-more.js' type='text/javascript'></script>
    <script src='http://code.highcharts.com/modules/exporting.js' type='text/javascript'></script>
    
    <style>
    .rChart {
      display: block;
      margin-left: auto; 
      margin-right: auto;
      width: 575px;
      height: 400px;
    }  
    </style>
    
  </head>
  <body >
    
    <div id = 'chart38dc94b056e' class = 'rChart highcharts'></div>    
    <script type='text/javascript'>
    (function($){
        $(function () {
            var chart = new Highcharts.Chart({
 "dom": "chart38dc94b056e",
"width":            575,
"height":            400,
"credits": {
 "href": null,
"text": null 
},
"exporting": {
 "enabled": false 
},
"title": {
 "text": null 
},
"yAxis": [
 {
 "title": {
 "text": "Number per month" 
} 
} 
],
"series": [
 {
 "data": [
 [
 new Date(2010,3,15),
             1 
],
[
 new Date(2010,4,15),
             0 
],
[
 new Date(2010,5,15),
             0 
],
[
 new Date(2010,6,15),
             0 
],
[
 new Date(2010,7,15),
             0 
],
[
 new Date(2010,8,15),
             4 
],
[
 new Date(2010,9,15),
             2 
],
[
 new Date(2010,10,15),
            12 
],
[
 new Date(2010,11,15),
             1 
],
[
 new Date(2011,0,15),
             2 
],
[
 new Date(2011,1,15),
             4 
],
[
 new Date(2011,2,15),
             2 
],
[
 new Date(2011,3,15),
             1 
],
[
 new Date(2011,4,15),
            13 
],
[
 new Date(2011,5,15),
             2 
],
[
 new Date(2011,6,15),
             0 
],
[
 new Date(2011,7,15),
             0 
],
[
 new Date(2011,8,15),
             4 
],
[
 new Date(2011,9,15),
            50 
],
[
 new Date(2011,10,15),
            24 
],
[
 new Date(2011,11,15),
             1 
],
[
 new Date(2012,0,15),
            63 
],
[
 new Date(2012,1,15),
            12 
],
[
 new Date(2012,2,15),
             2 
],
[
 new Date(2012,3,15),
             1 
],
[
 new Date(2012,4,15),
             3 
],
[
 new Date(2012,5,15),
             2 
],
[
 new Date(2012,7,15),
             0 
],
[
 new Date(2012,8,15),
             9 
],
[
 new Date(2012,9,15),
             4 
],
[
 new Date(2012,10,15),
            14 
],
[
 new Date(2012,11,15),
             1 
],
[
 new Date(2013,0,15),
             3 
],
[
 new Date(2013,1,15),
             0 
],
[
 new Date(2013,2,15),
             0 
],
[
 new Date(2013,3,15),
             0 
],
[
 new Date(2013,4,15),
            11 
],
[
 new Date(2013,5,15),
             2 
],
[
 new Date(2013,8,15),
             0 
],
[
 new Date(2013,9,15),
             1 
],
[
 new Date(2013,10,15),
             2 
],
[
 new Date(2013,11,15),
             1 
],
[
 new Date(2014,0,15),
             0 
],
[
 new Date(2014,1,15),
             0 
] 
],
"name": "comments",
"type": "line",
"marker": {
 "radius":              3 
} 
},
{
 "data": [
 [
 new Date(2010,3,15),
             1 
],
[
 new Date(2010,4,15),
             1 
],
[
 new Date(2010,5,15),
             1 
],
[
 new Date(2010,6,15),
             0 
],
[
 new Date(2010,7,15),
             0 
],
[
 new Date(2010,8,15),
            10 
],
[
 new Date(2010,9,15),
             3 
],
[
 new Date(2010,10,15),
            23 
],
[
 new Date(2010,11,15),
             2 
],
[
 new Date(2011,0,15),
            54 
],
[
 new Date(2011,1,15),
             1 
],
[
 new Date(2011,2,15),
             3 
],
[
 new Date(2011,3,15),
             5 
],
[
 new Date(2011,4,15),
            17 
],
[
 new Date(2011,5,15),
             0 
],
[
 new Date(2011,6,15),
             0 
],
[
 new Date(2011,7,15),
             0 
],
[
 new Date(2011,8,15),
            16 
],
[
 new Date(2011,9,15),
            66 
],
[
 new Date(2011,10,15),
            47 
],
[
 new Date(2011,11,15),
             8 
],
[
 new Date(2012,0,15),
            72 
],
[
 new Date(2012,1,15),
            20 
],
[
 new Date(2012,2,15),
             1 
],
[
 new Date(2012,3,15),
             5 
],
[
 new Date(2012,4,15),
             6 
],
[
 new Date(2012,5,15),
            23 
],
[
 new Date(2012,7,15),
             0 
],
[
 new Date(2012,8,15),
            54 
],
[
 new Date(2012,9,15),
            13 
],
[
 new Date(2012,10,15),
            12 
],
[
 new Date(2012,11,15),
             4 
],
[
 new Date(2013,0,15),
            28 
],
[
 new Date(2013,1,15),
            14 
],
[
 new Date(2013,2,15),
             8 
],
[
 new Date(2013,3,15),
            19 
],
[
 new Date(2013,4,15),
            99 
],
[
 new Date(2013,5,15),
            13 
],
[
 new Date(2013,8,15),
            32 
],
[
 new Date(2013,9,15),
            62 
],
[
 new Date(2013,10,15),
            43 
],
[
 new Date(2013,11,15),
             2 
],
[
 new Date(2014,0,15),
            20 
],
[
 new Date(2014,1,15),
             6 
] 
],
"name": "likes",
"type": "line",
"marker": {
 "radius":              3 
} 
},
{
 "data": [
 [
 new Date(2010,3,15),
             0 
],
[
 new Date(2010,4,15),
             0 
],
[
 new Date(2010,5,15),
             0 
],
[
 new Date(2010,6,15),
             0 
],
[
 new Date(2010,7,15),
             0 
],
[
 new Date(2010,8,15),
             0 
],
[
 new Date(2010,9,15),
             0 
],
[
 new Date(2010,10,15),
             0 
],
[
 new Date(2010,11,15),
             0 
],
[
 new Date(2011,0,15),
             0 
],
[
 new Date(2011,1,15),
             0 
],
[
 new Date(2011,2,15),
             0 
],
[
 new Date(2011,3,15),
             0 
],
[
 new Date(2011,4,15),
             0 
],
[
 new Date(2011,5,15),
             0 
],
[
 new Date(2011,6,15),
             0 
],
[
 new Date(2011,7,15),
             0 
],
[
 new Date(2011,8,15),
             0 
],
[
 new Date(2011,9,15),
             0 
],
[
 new Date(2011,10,15),
             0 
],
[
 new Date(2011,11,15),
             0 
],
[
 new Date(2012,0,15),
             3 
],
[
 new Date(2012,1,15),
             6 
],
[
 new Date(2012,2,15),
             0 
],
[
 new Date(2012,3,15),
             2 
],
[
 new Date(2012,4,15),
             2 
],
[
 new Date(2012,5,15),
             0 
],
[
 new Date(2012,7,15),
             0 
],
[
 new Date(2012,8,15),
             5 
],
[
 new Date(2012,9,15),
             4 
],
[
 new Date(2012,10,15),
             3 
],
[
 new Date(2012,11,15),
             0 
],
[
 new Date(2013,0,15),
             2 
],
[
 new Date(2013,1,15),
             2 
],
[
 new Date(2013,2,15),
             5 
],
[
 new Date(2013,3,15),
             1 
],
[
 new Date(2013,4,15),
             4 
],
[
 new Date(2013,5,15),
             0 
],
[
 new Date(2013,8,15),
             1 
],
[
 new Date(2013,9,15),
             2 
],
[
 new Date(2013,10,15),
             1 
],
[
 new Date(2013,11,15),
             0 
],
[
 new Date(2014,0,15),
             0 
],
[
 new Date(2014,1,15),
             0 
] 
],
"name": "shares",
"type": "line",
"marker": {
 "radius":              3 
} 
} 
],
"xAxis": [
 {
 "title": {
 "text": "Months since Jesus Bar page launched" 
} 
} 
],
"subtitle": {
 "text": null 
},
"id": "chart38dc94b056e",
"chart": {
 "renderTo": "chart38dc94b056e" 
} 
});
        });
    })(jQuery);
</script>
    
    <script></script>    
  </body>
</html>

[^1]: From Wikipedia: Betweenness centrality is a measure of a node's centrality in a network. It is equal to the number of shortest paths from all vertices to all others that pass through that node.
[^2]: The Tompkins score allocates 5 points for a First Class degree, 3 points for an Upper Second (known also as a 2.i), 2 points for a Lower Second (a 2.ii), 1 point for a Third and no points for someone only granted an allowance towards an Ordinary Degree.
[^3]: This also suggests I maybe should of looked at female as binary (all female or mixed).