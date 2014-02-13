---
layout: post
title: Visualising flow with a sankey plot
description: "Showing how to make a sankey plot using R."
category: articles
tags: [R, Sankey]
image: 
  thumb: sankey_thumb.png
  homepage: sankey_thumb.png
comments: true
share: true
---

<figure>
	<a href="/images/sankey_example.png"><img src="/images/sankey_example.png"></a>
	<figcaption>An example of the function output, taken from my thesis.</figcaption>
</figure>

Above is a Sankey plot that takes the number of individuals given the option of being
 screened for diabetes, and how individuals left the screening programme,
 till a fraction of the original number were diagnosed with diabetes.
 I’m using this figure in my PhD, and the numbers behind it come from a paper[^1] describing 
 a diabetes screening trial that was run by my supervisors.

The original Sankey diagram visualised the efficiency of a steam engine, 
but a more famous example is probably Minard’s picture of Napoleon’s disastrous Russian 
campaign (below). The general idea behind these plots is that the width of the arrows is 
to scale, so you can see the flow much more instinctively than a standard flow chart. 
Although Minard took it a step further by plotting it over a map, and also plotting the temperatures.

<figure>
	<a href="/images/sankey_minard.png"><img src="/images/sankey_minard.png"></a>
	<figcaption>Minard's summary of the failed Russian Campaign.</figcaption>
</figure>

The code is super simple to run. First the setup. We set the working directory, then set up
 a function to pull other functions and their dependencies from a Gist (an online repository).

{% highlight r %}
setwd("~/Dropbox/Personal/fun with code/sankey_arrow")
 
sourc.https     <- function(url, ...) {
  # install and load the RCurl package 
  if (match('RCurl', nomatch=0, installed.packages()[,1])==0) {
    install.packages(c("RCurl"), dependencies = TRUE)
    require(RCurl)  
  } else require(RCurl)    
  
  # parse and evaluate each .R script
  sapply(c(url, ...), function(u) {
    eval(parse(text = getURL(u, followlocation = TRUE, 
                             cainfo  = system.file("CurlSSL", "cacert.pem", 
                                                   package = "RCurl"))), envir = .GlobalEnv)
  } )
 
# from https://gist.github.com/1423501
sourc.https("https://gist.github.com/epijim/8832627/raw/91f8fb601a483a6e60c6cbc7eeea939e010cf7ce/Sankey.R")
}
{% endhighlight %} 

The last line of the previous code snippet read in the function to make the Sankey plot.
 I'm pulling it from my own Gist, rather than the official one, as I edited two lines that 
 effect how the text is written.
 
Then we just need to give the function the numbers that go in (inputs) and the numbers that
 go out. Then the labels in the same order. It's crazy simple!

{% highlight r %}
inputs = c(35297)
losses = c(1758,8885,23787,867)
unit = "n ="
 
labels = c("At high diabetes risk",
           "Did not meet criteria",
           "Did not attend screening",
           "Did not have diabetes",
           "Diagnosed with diabetes")
  pdf("Sankey.pdf", width=12, height=10)
    SankeyR(inputs,losses,unit,labels)
  dev.off()
{% endhighlight %}

[^1]: [Echouffo-Tcheugui et al(2009) BMC Public Health, 9:136](http://www.ncbi.nlm.nih.gov/pubmed/19435491)
